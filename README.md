# Conference Paper Setup Guide

## Conference Information
**Conference:** 2026 IEEE World Congress on Computational Intelligence (WCCI 2026)  
**Special Session:** IJCNN SS07 - Quantum Machine Learning Algorithms and Applications  
**Location:** Maastricht, Netherlands  
**Dates:** June 21-26, 2026  
**Submission Deadline:** January 31, 2026 (23:59 UTC-12)  
**Acceptance Notification:** March 15, 2026  
**Camera Ready:** April 15, 2026  

**Conference Website:** https://attend.ieee.org/wcci-2026/  
**Special Session:** https://sites.google.com/view/qml-wcci-2026/home

## Paper Title
**Equilibrium Propagation and Variational Quantum Circuits for Automated Detection of Acute Myeloid Leukemia from Blood Cell Microscopy Images**

## Quick Status Checklist
- [ ] LaTeX installed (TeXShop or MacTeX)
- [ ] IEEE conference .cls file (IEEEtran.cls) obtained and placed in this directory
- [ ] Author information updated in paper.tex (lines 15-25)
- [ ] Abstract reviewed (currently 220 words - within 150-250 range) ✓
- [ ] Keywords optimized for QML special session ✓
- [ ] Paper anonymized for double-blind review (remove author names before submission)
- [ ] Figures embedded and captions finalized ✓
- [ ] References updated with advisor's work
- [ ] Paper compiled to PDF successfully and verified ≤6 pages
- [ ] Code repository published (already at GitHub) ✓
- [ ] Paper submitted via WCCI submission system by Jan 31, 2026
- [ ] IEEE membership obtained for reduced registration

## Installation Steps

### 1. Install LaTeX (Choose one option)

**Option A: TeXShop (Recommended for Mac)**
1. Download MacTeX from: https://www.tug.org/mactex/
2. Install the full package (~4GB, includes TeXShop)
3. Open TeXShop from Applications

**Option B: Overleaf (Browser-based)**
1. Go to https://www.overleaf.com
2. Create a free account
3. Upload all files from this directory

### 2. Get IEEE Conference Template
1. Contact your conference organizers for the .cls file
2. OR download from: https://www.ieee.org/conferences/publishing/templates.html
3. Place `IEEEtran.cls` in this directory (same folder as paper.tex)

### 3. Update Paper Details
Open `paper.tex` and update:
- Lines 15-19: Your name, department, university, email
- Lines 21-25: Advisor's name and contact info
- Line 26: Add third author (Carsten Marr) if approved, otherwise delete the `\and` block

### 4. Compile the Paper

**Using TeXShop:**
1. Open `paper.tex` in TeXShop
2. Press Cmd+T to compile (or click "Typeset" button)
3. PDF will appear automatically
4. Fix any errors shown in console

**Using Overleaf:**
1. Upload all files including figures/ folder
2. Click "Recompile" button
3. PDF appears on right side

**Using Command Line:**
```bash
cd /Users/azrabano/conference-paper
pdflatex paper.tex
bibtex paper
pdflatex paper.tex
pdflatex paper.tex
```

## Current Paper Structure

### Abstract (Lines 32-33)
- **Length:** 220 words (within 150-250 range) ✓
- **Coverage:** Motivation, EP + VQC methods, comprehensive benchmarking, NISQ deployment ✓
- **Keywords:** 6 keywords optimized for WCCI QML special session ✓
  - equilibrium propagation
  - variational quantum circuits
  - quantum machine learning
  - medical image analysis
  - blood cell classification
  - acute myeloid leukemia

### Sections (Comprehensive Scientific Content)
1. **Introduction** - NISQ context, QML background, medical imaging challenges, AML dataset significance
2. **Methods**
   - Dataset and Preprocessing - WHO classification, stratified sampling, PCA for VQC
   - EP Framework - Free/nudged phase equations, 20 features, training hyperparameters
   - VQC Design - ZZFeatureMap math, RealAmplitudes ansatz, COBYLA optimization
   - Classical Baselines - Enhanced CNN, Dense NN specifications
3. **Results**
   - Overall Performance - Detailed metrics table with sample counts
   - Scaling Behavior - Data efficiency analysis across 4 dataset sizes
   - Computational Efficiency - Pareto frontier analysis
   - Clinical Metrics - Precision/recall/F1 table for EP and VQC
4. **Discussion** - Neuromorphic hardware, NISQ constraints, limitations, federated QML future directions
5. **Conclusions** - NISQ-era validation, translation to clinical practice
6. **Acknowledgments** - Dataset credit, code availability statement
7. **References** - 12 high-quality citations (Nature, IEEE, etc.)

### Figures Included
- `figure1_accuracy_comparison.png` - Accuracy across dataset sizes
- `figure2_efficiency_analysis.png` - Training time vs accuracy trade-off
- Additional figures available: figure3 (heatmap), figure4 (improvements)

## Next Steps for Friday Meeting (Jan 9, 3:30 PM)

### Before the Meeting:
1. Install LaTeX and compile the paper to PDF
2. Review the abstract and make minor edits if needed
3. Update author information with correct affiliations
4. Read through the full paper and note any technical corrections
5. Prepare 1-2 questions about tone/formatting for your advisor

### During the Meeting:
- Show the compiled PDF
- Get feedback on abstract and introduction tone
- Confirm which figures to include (currently using 2 of 4)
- Verify technical accuracy of EP and VQC descriptions
- Ask about adding Carsten Marr as third author
- Get advisor's papers to cite in references

### After the Meeting:
- Incorporate feedback from advisor
- Add 2-3 more references (aim for 8-10 total)
- Consider adding figure3 or figure4 if space permits
- Verify page count is ≤6 pages
- Polish figures if resolution/labels need improvement

## Conference Logistics

### IMPORTANT: Double-Blind Review
WCCI 2026 uses **double-blind review**. Before submitting:
1. Remove author names and affiliations from paper.tex (lines 14-26)
2. Remove Acknowledgments section (or anonymize it)
3. Do NOT include identifying information in PDF metadata
4. Keep code repository link in final camera-ready version only

### IEEE Membership (Recommended)
1. Visit: https://www.ieee.org/membership
2. Select "Student Member" (~$32/year) or "Graduate Student Member"
3. Join IEEE Computational Intelligence Society (CIS) as well for additional discount
4. Use membership number during conference registration for reduced fees

### Conference Registration
1. Paper must be **accepted first** (notification: March 15, 2026)
2. Register by early registration deadline (typically ~April 15)
3. At least one author must register and present
4. Student registration rates available (~€400-600)
5. Registration covers conference proceedings and IEEE Xplore publication

### Travel to Maastricht
- **Flights:** Nearest airport is Maastricht Aachen Airport (MST) or Amsterdam Schiphol (AMS, 2.5h train)
- **Accommodation:** Book early (June is peak conference season)
- **Visa:** Check if you need Schengen visa (apply 3+ months in advance)

### Travel Grants
Consider applying for:
- IEEE CIS Student Travel Grants (check CIS website for deadlines)
- University research/conference travel funds
- NSF or other federal student grants
- Graduate student organization funding
- Reference your NASA and Rutgers support in applications
- **Deadline:** Most travel grants require 2-3 months notice, apply by March 2026

## Technical Details

### Page Limit
- Maximum: 6 pages (including references and figures)
- Current draft should be close to limit once compiled

### Required Format
- IEEE conference format (two-column)
- 10pt font
- Single-spaced
- Figures can span one or two columns

### Citation Style
- IEEE citation style (numbered references)
- Format: \cite{AuthorYear} in text
- Bibliography at end with \bibitem

## Files in This Directory

```
conference-paper/
├── paper.tex              # Main LaTeX document
├── README.md             # This file
├── figures/              # All figure files
│   ├── figure1_accuracy_comparison.png
│   ├── figure2_efficiency_analysis.png
│   ├── figure3_heatmap_summary.png
│   └── figure4_improvements.png
└── IEEEtran.cls          # IEEE template (add this file)
```

## Common LaTeX Errors and Fixes

**Error:** "IEEEtran.cls not found"
- **Fix:** Download IEEEtran.cls and place in same folder as paper.tex

**Error:** "figures/figure1.png not found"
- **Fix:** Ensure figures/ folder is in the same directory

**Error:** "Undefined control sequence"
- **Fix:** Check for typos in LaTeX commands (e.g., \textbf vs \textbold)

**Error:** "Missing $ inserted"
- **Fix:** Mathematical symbols need to be in math mode: $x$ not just x

## LaTeX Quick Reference

### Common Commands
- `\section{Title}` - Section heading
- `\textit{text}` - Italic text
- `\textbf{text}` - Bold text
- `\cite{key}` - Citation reference
- `$math$` - Inline math
- `\begin{equation}...\end{equation}` - Display equation
- `%` - Comment (line ignored)

### Figures
```latex
\begin{figure}[h]
\centering
\includegraphics[width=0.48\textwidth]{figures/filename.png}
\caption{Description of figure.}
\label{fig:shortname}
\end{figure}
```

### Tables
```latex
\begin{table}[h]
\caption{Table title}
\label{tab:name}
\begin{tabular}{|l|c|r|}
\hline
Left & Center & Right \\
\hline
Data & Data & Data \\
\hline
\end{tabular}
\end{table}
```

## Getting Help

### LaTeX Resources
- Overleaf tutorials: https://www.overleaf.com/learn
- LaTeX Wikibook: https://en.wikibooks.org/wiki/LaTeX
- IEEE template guide: https://www.ieee.org/conferences/publishing/templates.html

### Questions?
- Ask your advisor during Friday meeting
- TeXShop Help menu
- Stack Exchange (TeX): https://tex.stackexchange.com

## Important Reminders

1. **Co-authorship credit:** Add `Co-Authored-By: Warp <agent@warp.dev>` if you commit this work to version control
2. **Deadline awareness:** Confirm paper submission deadline with advisor
3. **Backup your work:** Use Git or cloud storage for version control
4. **Print before meeting:** Have a physical copy for Friday meeting if possible

Good luck with your paper! You have a solid draft ready to refine.
