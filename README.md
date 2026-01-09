# Conference Paper Setup Guide

## Paper Title
**Equilibrium Propagation and Variational Quantum Circuits for Medical Image Analysis**

## Quick Status Checklist
- [ ] LaTeX installed (TeXShop or MacTeX)
- [ ] IEEE conference .cls file obtained and placed in this directory
- [ ] Author information updated in paper.tex
- [ ] Abstract reviewed and keywords finalized
- [ ] Figures reviewed and captions adjusted if needed
- [ ] References updated with advisor's work
- [ ] Paper compiled to PDF successfully
- [ ] INNS membership obtained
- [ ] Conference registration completed

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

### Abstract (Lines 32-34)
- **Length:** 216 words (within 150-250 range) ✓
- **Coverage:** Motivation, methods, results, implications ✓
- **Keywords:** 6 keywords listed ✓

### Sections
1. **Introduction** - Context, gap, contributions
2. **Methods** - Dataset, EP framework, VQC design, baselines
3. **Results** - Performance tables, scaling behavior, efficiency
4. **Discussion** - Interpretation, limitations, future work
5. **Conclusions** - Summary of contributions
6. **References** - 7 citations (add 2-3 more including advisor's work)

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

### INNS Membership
1. Visit: https://www.inns.org/membership
2. Select "Student Member" (~$15/year)
3. Complete registration and payment
4. Save membership confirmation

### Conference Registration
1. After INNS membership is confirmed
2. Register for conference in Maastricht
3. Use student member discount code
4. Register early for best rates

### Travel Grants
Consider applying for:
- INNS student travel grants
- University research travel funds
- NSF or other federal student grants
- Reference your NASA and Rutgers support in applications

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
