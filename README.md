## GenderRx — Clinical Bias Auditor

> **Gender-neutral does not mean fair.**
> An open-source clinical decision support tool that detects gender bias in medical prescriptions — in real time, at the point of prescribing.

![License](https://img.shields.io/badge/license-MIT-green)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/vanilla%20JS-F7DF1E?logo=javascript&logoColor=black)
![Dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen)
![Open Source](https://img.shields.io/badge/open%20source-yes-blue)

---

## Table of Contents

- [The Problem](#-the-problem)
- [How It Works](#-how-it-works)
- [Features](#-features)
- [Screenshots](#-screenshots)
- [Getting Started](#-getting-started)
- [Tech Stack](#-tech-stack)
- [Data Sources & References](#-data-sources--references)
- [Project Structure](#-project-structure)
- [Roadmap](#-roadmap)
- [License](#-license)

---

##  The Problem

Medical prescriptions are designed using male-centric clinical trial data. Women metabolize drugs differently — but dosing guidelines rarely reflect it.

| Fact | Source |
|------|--------|
| Women metabolize zolpidem **45% slower** — the FDA cut the female dose to 5mg in 2013 | FDA Drug Safety Communication (2013) |
| Women need **30% lower** warfarin doses for the same therapeutic effect | Holbrook et al., *Chest*, 2012 |
| Women have **36% lower** renal clearance of digoxin — toxicity occurs 36% more often | DIG Trial, *Lancet*, 1997 |
| Women have **1.7× higher** risk of NSAID-induced GI complications | Warner et al., 2017 |
| Millions of adverse drug reaction hospitalizations each year are linked to sex-incorrect dosing | WHO |
| In one tragic postpartum case, a woman was prescribed **13 psychiatric drugs in 4 months** — three benzodiazepines simultaneously — with no system flagging the dangerous polypharmacy | PBS NewsHour, 2023 |

**No existing tool cross-references a prescription against sex-specific pharmacokinetics, patient risk factors, allergies, and condition appropriateness — all in one place.** That is the gap GenderRx fills.

---

##  How It Works

```
Prescription input          Cross-referencing engine           Evidence-cited output
─────────────────          ─────────────────────────          ─────────────────────
Drug + dose        ──┐
Patient sex/age    ──┤     • Sex-specific dosing rules        Bias Risk Score (0–10)
Risk factors       ──┼──▶  • Allergy cross-reactivity    ──▶  • Alert cards with severity
Allergies          ──┤     • Drug–condition matching          • Safer alternatives for women
Condition          ──┘     • Pregnancy/lactation categories   • Citation for every claim
```

Every prescription receives a **Bias Risk Score from 0 to 10**. Alerts are graded (high / medium / low), each carries a concrete recommendation, and each one cites its source — so a clinician can verify, not just trust.

---

##  Features

### Five modules

| Module | Description |
|--------|-------------|
|  **Dashboard** | Live statistics — audits run, bias flagged, average risk score, trend chart and risk distribution |
|  **Prescription Analyzer** | Audits a prescription against gender-specific dosing, allergies, patient risk factors, and indication appropriateness |
|  **Hormonal Cycle Adjuster** | Pregnancy trimester, lactation, and menopause status → FDA-category-based dosage adjustments |
|  **Drug Bias Database** | Searchable profiles for every drug: male vs. female dose, bias score, mechanism, interactions, references |
|  **Audit Log** | Complete history of every analysis with CSV export |

### Detection capabilities

- **40+ drug profiles** with sex-specific pharmacokinetics — male dose, female dose, bias score, mechanism, and citation
- **12 patient risk factors** — hypokalemia, kidney/liver disease, HSP history, diabetes, asthma, and more — cross-referenced against the prescribed drug
- **25+ allergy categories** with direct-match and cross-reactivity detection (e.g. penicillin → cephalosporin, latex → banana/avocado/kiwi)
- **Indication appropriateness** — flags antibiotics prescribed for viral infections, per WHO antimicrobial resistance guidelines
- **Pregnancy & lactation engine** — FDA pregnancy categories (X → contraindicated, D, C, B, A) with automatic dose recalculation
- **Brand-name resolution** — type `Dolo 650`, `Azithral`, `Combiflam`, `Crocin`… common brands map to their generic entries automatically
- **Safer alternatives** — every high-bias finding suggests a lower-risk option for female patients

---

###  Dashboard — live audit statistics & risk trends
![Dashboard](screenshots/01-dashboard.png)

###  Prescription Analyzer — HIGH BIAS RISK (9.0) detected
![Analyzer — high bias risk](screenshots/02-analyzer-high-risk.png)

###  Risk factors, allergies & safer alternatives
![Risk factors and allergies](screenshots/04-risk-and-allergies.png)

###  Drug Bias Database — sex-specific dosing at a glance
![Drug database](screenshots/03-drug-database.png)

###  Hormonal Cycle Adjuster — pregnancy-aware dosage adjustment
![Hormonal adjuster](screenshots/05-hormonal-adjuster.png)

---

##  Getting Started

No build step, no install, no dependencies.

```bash
git clone https://github.com/<your-username>/genderrx.git
cd genderrx
# open index.html in any browser — that's it
```

Or simply download [`index.html`](./index.html) and double-click it. It runs fully offline.

**Try this demo scenario:** Prescription Analyzer → drug `Azithromycin`, dose `500`, sex `Female`, condition `Flu (Viral)`, risk factor `Low Potassium` → **Analyze**. You'll get a 9.0 HIGH BIAS RISK result with a QT-prolongation alert and safer alternatives.

---

##  Tech Stack

| Layer | Choice |
|-------|--------|
| Frontend | Vanilla HTML5, CSS3, JavaScript (ES6) |
| Styling | CSS custom properties, grid & flexbox — no framework |
| Charts | Pure CSS/JS (no charting library) |
| Data | Inline rules engine — fully transparent and auditable |
| Dependencies | **Zero** |

**Production roadmap stack:** React · Node.js REST API · Python (FastAPI) pharmacokinetic rules engine · MongoDB knowledge graph · NLP pipeline mining FDA FAERS and peer-reviewed literature for new bias signals.

---

##  Data Sources & References

1. FDA Drug Safety Communication — Zolpidem dosing recommendation (2013)
2. Holbrook et al., Warfarin dosing and outcomes, *Chest*, 2012
3. DIG Trial, Digoxin, *The Lancet*, 1997
4. Warner et al., NSAID gastrointestinal risk, 2017
5. Ridker et al., Aspirin sex-specific efficacy, *NEJM*, 2005
6. Makrilakis et al., QT prolongation with macrolides, 2014
7. WHO — Antimicrobial Resistance Guidelines
8. WHO — Adverse Drug Reactions
9. PBS NewsHour — postpartum polypharmacy case coverage (2023)
10. The Boston Globe — polypharmacy investigation (2023)

---

##  Project Structure

```
genderrx/
├── index.html              # The complete application (single file)
├── README.md               # This file
└── screenshots/            # Demo screenshots
    ├── 01-dashboard.png
    ├── 02-analyzer-high-risk.png
    ├── 03-drug-database.png
    ├── 04-risk-and-allergies.png
    └── 05-hormonal-adjuster.png
```

---

##  Roadmap

- [ ] Integrate a real drug-interaction API (OpenFDA / RxNorm)
- [ ] Add pediatric and geriatric dosing engines
- [ ] Browser/EHR plugin for point-of-care alerts
- [ ] Expand the database to 200+ drugs with automated literature mining
- [ ] Multilingual UI (Hindi, Marathi)
- [ ] Dark mode

---

##  Contributing

Contributions are welcome — especially new drug profiles with peer-reviewed citations.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-drug`)
3. Commit your changes (`git commit -m 'Add drug profile: ...'`)
4. Open a Pull Request

Please attach a credible source (FDA communication or peer-reviewed paper) for any clinical data you add.

---

##  License

MIT — free to use, fork, and improve.

---

<p align="center">Built to make prescribing fairer — for everyone.</p>
