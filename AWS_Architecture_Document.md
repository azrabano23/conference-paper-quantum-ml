# EndoDetect AI - AWS Architecture & Resource Justification

## Executive Summary
EndoDetect AI is a research prototype platform for AI-assisted endometriosis detection using medical imaging (MRI and transvaginal ultrasound). This document outlines the AWS resources required for **model development, training, and internal validation** - NOT clinical deployment.

---

## System Architecture Overview

### Current State
- **Frontend-only React + Vite demo** with mocked data
- No backend or ML processing implemented
- Demo URL: [To be provided]

### Planned AWS Architecture (Research Phase)

```
┌─────────────────────────────────────────────────────────────────┐
│                          USER LAYER                              │
│  Research Team (Developers, Data Scientists, Clinicians)        │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                     API/ORCHESTRATION LAYER                      │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  AWS API Gateway + Lambda Functions                       │  │
│  │  - Image upload endpoints                                 │  │
│  │  - Model inference triggers                               │  │
│  │  - Metadata retrieval                                     │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────┬───────────────────────────────────┘
                              │
                ┌─────────────┴─────────────┐
                ▼                           ▼
┌───────────────────────────┐   ┌───────────────────────────────┐
│     STORAGE LAYER         │   │   COMPUTE/ML LAYER            │
│  ┌─────────────────────┐  │   │  ┌─────────────────────────┐ │
│  │   AWS S3 Buckets    │  │   │  │  EC2 GPU Instances      │ │
│  │                     │  │   │  │  - Model training       │ │
│  │  • Raw imaging data │  │   │  │  - nnU-Net             │ │
│  │    (MRI/TVUS)      │  │   │  │  - RAovSeg             │ │
│  │  • De-identified   │  │   │  │  - Ensemble models     │ │
│  │  • Encrypted       │  │   │  └─────────────────────────┘ │
│  │  • Versioned       │  │   │             OR                │
│  │                     │  │   │  ┌─────────────────────────┐ │
│  │  • Processed data  │  │   │  │  SageMaker              │ │
│  │  • Model outputs   │  │   │  │  - Managed training     │ │
│  │  • Segmentation    │  │   │  │  - Experiment tracking  │ │
│  │    masks           │  │   │  │  - Model versioning     │ │
│  └─────────────────────┘  │   │  └─────────────────────────┘ │
└───────────────────────────┘   └───────────────────────────────┘
                │                               │
                └───────────────┬───────────────┘
                                ▼
                ┌───────────────────────────────┐
                │   METADATA/TRACKING LAYER     │
                │  ┌─────────────────────────┐  │
                │  │  DynamoDB / RDS         │  │
                │  │  - Experiment metadata  │  │
                │  │  - Model performance    │  │
                │  │  - Patient IDs (hashed) │  │
                │  │  - Annotation tracking  │  │
                │  └─────────────────────────┘  │
                └───────────────────────────────┘
```

---

## Detailed Resource Requirements & Justification

### 1. **AWS S3 (Simple Storage Service)**
**Purpose:** Secure storage of de-identified medical imaging data

**What We'll Store:**
- MRI scans (pelvic, multi-sequence)
- Transvaginal ultrasound (TVUS) images
- Segmentation masks and annotations
- Model checkpoints and outputs

**Why We Need It:**
- Medical images are large (50-500 MB per patient scan)
- Need versioning for reproducibility
- Built-in encryption (SSE-S3 or SSE-KMS)
- Access control via IAM policies
- Estimated storage: **~200 patients × 200 MB/patient = 40 GB initially**

**Security:**
- Server-side encryption enabled
- Bucket policies restricting access to research team only
- No public access
- Audit logging via CloudTrail

---

### 2. **AWS EC2 (Elastic Compute Cloud) with GPU**
**Purpose:** Model training and inference for deep learning segmentation

**What We'll Run:**
- **nnU-Net** (state-of-the-art medical image segmentation)
- **RAovSeg** (custom Attention U-Net + ResNet pipeline)
- **Ensemble models** combining multiple resolutions
- PyTorch/TensorFlow training scripts
- PyRadiomics feature extraction

**Why We Need It:**
- Deep learning models require GPU acceleration (NVIDIA A100 or similar)
- Training on 30-80 MRI cases + augmentation = **50-100 hours of compute**
- Each model iteration requires 8-16 GB GPU memory
- Need for hyperparameter tuning and ablation studies

**Instance Types Needed:**
- **Development:** `g4dn.xlarge` (1 GPU, 16 GB memory) - $0.526/hour on-demand
- **Training:** `p3.2xlarge` (1 V100 GPU, 16 GB memory) - $3.06/hour on-demand
- **Alternative:** SageMaker training jobs (see below)

**Estimated Usage:**
- 200 hours of training over 3 months = ~$600-1,000

---

### 3. **AWS SageMaker (Alternative to EC2)**
**Purpose:** Managed ML platform for model development and tracking

**What We'll Use:**
- **SageMaker Training Jobs:** Managed training with automatic resource scaling
- **SageMaker Notebooks:** Jupyter notebooks for experimentation
- **SageMaker Experiments:** Track model versions, hyperparameters, and metrics
- **SageMaker Model Registry:** Version control for trained models

**Why We Need It:**
- **Reproducibility:** Automatic experiment tracking (critical for research)
- **Collaboration:** Shared notebooks and model artifacts
- **Cost Efficiency:** Pay only for training time (spot instances possible)
- **Built-in MLOps:** Model versioning and metadata tracking

**Trade-off vs. EC2:**
- SageMaker is more expensive per hour BUT easier to manage and track
- Better for research environments with multiple collaborators

---

### 4. **AWS Lambda + API Gateway**
**Purpose:** Lightweight API for image upload and model inference orchestration

**What We'll Build:**
- `/upload` endpoint: Accept de-identified images from frontend
- `/segment` endpoint: Trigger model inference
- `/results` endpoint: Retrieve segmentation masks and confidence scores

**Why We Need It:**
- **Serverless:** No need to manage infrastructure
- **Cost-effective:** Pay per request (estimated <$10/month for prototype)
- **Scalable:** Automatically handles multiple requests
- **Security:** Integrate with AWS IAM and VPC for secure access

**Use Case Example:**
1. User uploads MRI via React frontend
2. Lambda function validates and stores image in S3
3. Lambda triggers SageMaker inference endpoint
4. Results returned to frontend as JSON (lesion coordinates, heat map)

---

### 5. **AWS RDS (Relational Database Service) or DynamoDB**
**Purpose:** Store experiment metadata and tracking information

**What We'll Store:**
- Patient metadata (de-identified IDs, scan dates, stage classification)
- Model training logs (loss curves, Dice scores, inference time)
- Annotation provenance (which rater labeled which images)
- Experiment configurations (hyperparameters, data splits)

**Why We Need It:**
- Need structured storage for reproducible research
- RDS (PostgreSQL) for relational queries
- DynamoDB for NoSQL flexibility (better for rapid prototyping)

**Estimated Cost:**
- RDS `db.t3.micro`: ~$15/month
- DynamoDB on-demand: <$5/month for low volume

---

### 6. **IAM (Identity and Access Management)**
**Purpose:** Secure access control for team members

**What We'll Configure:**
- **Students:** Read/write access to S3 (specific folders), SageMaker notebooks
- **Clinicians:** Read-only access to anonymized data and model outputs
- **PIs:** Full administrative access

**Why We Need It:**
- HIPAA compliance requires strict access controls
- Audit trail via CloudTrail
- Multi-factor authentication (MFA) enforcement

---

## Data Flow Example: Training Pipeline

```
1. Clinician uploads de-identified MRI → S3 bucket (encrypted)
2. Data scientist triggers training job via SageMaker
3. SageMaker pulls data from S3, trains nnU-Net on GPU instance
4. Model outputs (segmentation masks) saved back to S3
5. Metadata (Dice score, training time) logged to RDS/DynamoDB
6. Frontend demo fetches results from S3 via API Gateway
```

---

## Security & Compliance

### HIPAA Considerations
- All data **de-identified** before upload (no PHI)
- S3 buckets encrypted at rest (AES-256)
- Data transfer encrypted via HTTPS (TLS 1.2+)
- Access logs via CloudTrail and S3 access logging
- VPC isolation for EC2/SageMaker (no public internet access)

### IRB Alignment
- AWS resources used **only for research** (not clinical diagnosis)
- Data sharing agreements with Rutgers and UCSF
- IRB protocol to be submitted once LOI approved

---

## Cost Estimate (3-Month Pilot)

| Resource | Estimated Cost |
|----------|---------------|
| S3 Storage (50 GB) | $1-2/month |
| EC2/SageMaker Training | $600-1,000 total |
| Lambda + API Gateway | $10-20/month |
| RDS/DynamoDB | $15-20/month |
| Data Transfer | $20-50/month |
| **TOTAL (3 months)** | **~$750-1,200** |

---

## Why We Can't Do Anything Without These Resources

### Current State (No AWS):
❌ Cannot store real medical imaging data securely  
❌ Cannot train deep learning models (require GPU)  
❌ Cannot run inference on new images  
❌ Cannot track experiments or model versions  
❌ Demo is static with fake data  

### With AWS Resources:
✅ Securely store 200+ de-identified patient scans  
✅ Train nnU-Net, RAovSeg, and ensemble models  
✅ Generate real segmentation outputs (heat maps, lesion masks)  
✅ Track model performance (Dice scores, sensitivity/specificity)  
✅ Build end-to-end pipeline for **Maternal Health Awareness Day demo** (Jan 23)  
✅ Validate model on held-out test set (8 patients)  
✅ Prepare for full grant submission with preliminary results  

---

## Timeline Alignment with Competition (Jan 23, 2026)

### Week of Jan 13-17:
- Receive AWS credits
- Set up S3 buckets and IAM roles
- Upload first batch of de-identified data (30 patients)

### Week of Jan 17-23:
- Train initial nnU-Net baseline on EC2/SageMaker
- Generate segmentation outputs for demo
- Integrate model outputs into React frontend
- **Mock presentation:** Jan 17
- **Final pitch:** Jan 23, 11am-12pm

---

## Technical Stack Summary

| Component | Technology |
|-----------|-----------|
| Frontend | React + Vite (current demo) |
| Backend | AWS Lambda + API Gateway |
| Storage | AWS S3 (encrypted, versioned) |
| Compute | EC2 (GPU) or SageMaker Training |
| Database | RDS (PostgreSQL) or DynamoDB |
| ML Frameworks | PyTorch, nnU-Net, PyRadiomics |
| Segmentation | U-Net, Attention U-Net, ResNet |

---

## Conclusion

**Without AWS resources, we cannot:**
- Train AI models on real data
- Generate actual segmentation outputs
- Demonstrate technical feasibility
- Compete effectively on Jan 23

**With AWS resources, we can:**
- Build a working prototype in 10 days
- Showcase real segmentation results
- Validate our approach with quantitative metrics
- Position ourselves for full grant funding

**This is a research prototype, NOT a clinical tool.** All work aligns with IRB protocols and data use agreements.

---

## Contact Information
- **PI:** Dr. Jessica Opoku-Anane (Rutgers RWJMS)
- **Co-I:** Dr. Archana Pradhan (Rutgers OBGYN)
- **Co-I:** Dr. Naveena Yanamala (AI/ML Lead)
- **Student Lead:** Azra Bano (azra.bano@rutgers.edu)

---

**Prepared for AWS Educate Credit Request**  
**Date:** January 12, 2026  
**Competition:** Maternal Health Awareness Day Pitch (Jan 23, 2026)
