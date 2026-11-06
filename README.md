# ats-ledger

**Deterministic 100-Point Enterprise ATS Parsing Engine & Mathematical Resume Scorecard**

`ats-ledger` (`offline_ats_auditor.py`) is a standalone, zero-dependency Python 3 CLI and auditing engine modeled on enterprise Applicant Tracking Systems (**Textkernel/Sovren, Workday, iCIMS, Taleo, and Eightfold.ai**).

Unlike black-box LLM resume graders that guess percentages or hallucinate feedback, `ats-ledger` calculates your score deterministically using a transparent **5-Component, 100-Point Algorithmic Formula**, quotes the exact supporting line from your resume for every requirement, and ranks your missing or penalized keywords by **exact recoverable ATS points**.

---

## Key Features

- **Zero External Dependencies:** Runs offline on standard Python 3.8+ (`dataclasses`, `re`, `datetime`, `json`, `argparse`).
- **Dual ATS Scoring Engine:** Computes both **Modern Semantic ATS Scores** (Workday / Eightfold / Textkernel, where synonyms earn `0.5x` credit) and **Legacy Literal-Only Boolean Scores** (Taleo / iCIMS, where synonyms earn `0.0x`).
- **HR-XML Section & Tenure Parser:** Segments plain-text or Markdown resumes into standard HR-XML zones (`Professional Summary`, `Work Experience`, `Education`, `Certifications`, `Technical & Core Skills`), parses `MM/YYYY` and `Month YYYY` role dates, calculates exact domain tenure in years, and separates recent roles (<= 5 years) from historical roles (> 5 years).
- **Sovren/Textkernel Contextual Placement Penalties:** Penalizes "keyword stuffing" in standalone bottom Skills sections (`0.4x` multiplier) vs. verified usage inside recent Work Experience bullets (`1.0x` multiplier) or older historical roles (`0.8x` multiplier).
- **Knockout Gate Verification:** Automatically flags `AUTO-REJECT GATE TRIGGERED` if mandatory degrees, licenses, clearances, or work-authorization gates are missing.
- **Highest-ROI Point Recovery Plan:** Ranks every gap or penalized match by exact composite points lost across **Tier 1** (`0.5x -> 1.0x` synonym-to-literal swaps), **Tier 2** (`0.4x -> 1.0x` skills-list-to-bullet elevations), and **Tier 3** (`0.0x` true gap checks).

---

## Quick Start

### 1. Run the Built-In Verification Demo
```bash
git clone https://github.com/<your-username>/ats-ledger.git
cd ats-ledger
python3 offline_ats_auditor.py --demo
```

### 2. Audit a Resume Against a Structured JD JSON Config
```bash
python3 offline_ats_auditor.py \
  --resume my_resume.txt \
  --jd-config jd_rules.json \
  --output audit_report.md \
  --json-out audit_report.json
```

### 3. Audit a Resume Against a Plain-Text Job Description
```bash
python3 offline_ats_auditor.py \
  --resume my_resume.txt \
  --jd-text job_description.txt \
  --output audit_report.md
```

---

## License

MIT License
