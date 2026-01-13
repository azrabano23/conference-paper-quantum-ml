# AWS Resource Request - EndoDetect AI
## One-Page Executive Summary

**Project:** EndoDetect AI - AI-Assisted Endometriosis Detection  
**Institution:** Rutgers Robert Wood Johnson Medical School  
**Competition:** Maternal Health Awareness Day Pitch (January 23, 2026)  
**Student Lead:** Azra Bano | Faculty Advisors: Dr. Opoku-Anane, Dr. Pradhan, Dr. Yanamala

---

## The Problem
Endometriosis affects 190 million women globally with 7-10 year diagnostic delays. We're building an AI system to detect endometriosis from MRI/ultrasound images, but **we currently have only a static frontend demo with fake data**. Without AWS resources, we cannot train models or generate real outputs.

---

## What We Need From AWS

| Resource | Purpose | Why Critical |
|----------|---------|--------------|
| **S3 Storage** | Store 40GB of de-identified MRI/ultrasound images | Cannot train models without secure data storage |
| **EC2 GPU Instances** | Train nnU-Net deep learning models | Requires NVIDIA GPUs (200 hours compute) |
| **SageMaker** | Managed ML training + experiment tracking | Track model versions for reproducibility |
| **Lambda + API Gateway** | Connect frontend demo to ML backend | Cannot run inference without API layer |
| **RDS/DynamoDB** | Store model performance metrics | Need to log Dice scores, accuracy, etc. |

**Estimated Cost:** $750-1,200 over 3 months

---

## Why We Can't Login and "Do Nothing"

### Current State (No AWS Access):
- ❌ Cannot store real patient imaging data
- ❌ Cannot train deep learning models (no GPU)
- ❌ Cannot run inference on new images
- ❌ Demo shows only mocked data
- ❌ Cannot compete on January 23

### With AWS Resources:
- ✅ Upload 30-80 de-identified patient scans to S3
- ✅ Train nnU-Net segmentation model on EC2/SageMaker
- ✅ Generate real lesion detection outputs (heat maps)
- ✅ Integrate trained model with React frontend
- ✅ **Demo working prototype at competition**

---

## Architecture Overview

```
Research Team
     ↓
API Gateway + Lambda (upload images, trigger inference)
     ↓
S3 Storage (40GB MRI/TVUS images, encrypted)
     ↓
EC2/SageMaker (train nnU-Net on GPU: 200 hours)
     ↓
RDS (log model performance: Dice score, accuracy)
     ↓
Frontend Demo (React app shows real segmentation results)
```

---

## Timeline to January 23 Competition

**Week 1 (Jan 13-17):**
- Set up S3 buckets, IAM roles, VPC
- Upload first 30 patient scans
- Start nnU-Net training on EC2

**Week 2 (Jan 17-23):**
- Complete model training
- Generate segmentation outputs
- Integrate with frontend
- **Jan 17:** Mock presentation with AWS team
- **Jan 23:** Final pitch (11am-12pm, 180-person audience)

---

## Security & Compliance
- All data **de-identified** (no PHI)
- S3 encrypted at rest (AES-256)
- HTTPS/TLS for transit
- IAM role-based access
- IRB protocol pending full grant award

---

## This Is Research, Not Clinical Deployment
- ✓ For model development and validation only
- ✓ Internal testing with 30-80 cases
- ✓ Support grant application to Nuttall Women's Health ($4M LOI submitted)
- ✗ NOT patient-facing
- ✗ NOT for clinical diagnosis

---

## Bottom Line
**Without AWS, we have a static demo with fake data and cannot compete.**  
**With AWS, we can train real models, generate actual outputs, and showcase technical feasibility in 10 days.**

This is why we need the architecture approved and credits allocated urgently.

---

**Contact:**  
Azra Bano - azra.bano@rutgers.edu  
Dr. Archana Pradhan - ap2556@rwjms.rutgers.edu  
Dr. Naveena Yanamala - naveena.yanamala@rutgers.edu
