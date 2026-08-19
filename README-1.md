# 🧬 Computational Oncology Study: p53 & KRAS G12D

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)
![Biopython](https://img.shields.io/badge/Biopython-1.85-0F6E56?style=flat-square)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-534AB7?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📋 Overview

This repository contains an independent computational oncology research project (May–June 2026) centered on a unified scientific theme: the **p53/KRAS G12D oncogenic axis** — two of the most critical proteins in human cancer biology.

The project spans sequence analysis, evolutionary conservation, multiple sequence alignment, and a comprehensive review of how bioinformatics unlocked the first clinical inhibitors of KRAS G12D — previously considered **undruggable for 40 years**.

> **Author:** Charles Arnaud Jesutin Hounsou-Kan  
> **Background:** Medical Biotechnology — Specialization toward Medical Data Science  
> **Goal:** PhD applications in Computational Oncology / Quantitative Biology (USA)

---

## 🎯 Scientific Context

| Protein | Gene | UniProt | Role in Cancer |
|---------|------|---------|----------------|
| p53 | TP53 | [P04637](https://www.uniprot.org/uniprot/P04637) | Tumor suppressor — inactivated in ~50% of all cancers |
| KRAS (WT) | KRAS | [P01116](https://www.uniprot.org/uniprot/P01116) | Proto-oncogene — mutated in ~25% of all cancers |
| KRAS G12D | KRAS | — | Dominant mutation: ~42% PDAC, ~13% CRC, ~5% NSCLC |

---

## 📁 Repository Structure

```
KRAS-G12D-Computational-Oncology/
│
├── README.md
│
├── Task1_BLAST/
│   ├── KRAS_Task1_BLAST.ipynb            # Python notebook: sequence download + BLAST
│   ├── KRAS_Task1_BLAST_Report.pdf       # 3-page analysis report
│   ├── p53_human.fasta                   # p53 sequence (UniProt P04637)
│   ├── kras_human.fasta                  # KRAS WT sequence (UniProt P01116)
│   ├── blast_p53_results.xml             # Raw BLAST XML output
│   ├── blast_kras_results.xml            # Raw BLAST XML output
│   ├── blast_p53_identity.png            # Conservation bar chart — p53
│   ├── blast_kras_identity.png           # Conservation bar chart — KRAS
│   └── blast_combined_results.csv        # Parsed results table
│
├── Task2_MSA/
│   ├── KRAS_Task2_MSA.ipynb              # Python notebook: MSA + G12D analysis
│   ├── KRAS_Task2_MSA_Report.pdf         # 3-page alignment report
│   ├── kras_5species_input.fasta         # Multi-FASTA input (5 species)
│   ├── kras_msa_aligned.fasta            # Clustal Omega alignment output
│   ├── kras_msa_conservation.png         # Conservation profile + G12 hotspot
│   └── kras_identity_matrix.png          # Pairwise identity heatmap
│
└── Task3_DrugDiscovery/
    └── KRAS_Task3_DrugDiscovery_Report.pdf  # 6-page literature review report
```

---

## 🔬 Task 1 — DNA/Protein Sequence Analysis (BLAST)

**Objective:** Retrieve p53 and KRAS wild-type sequences from UniProt and perform comparative BLAST analysis against mammalian species to quantify evolutionary conservation.

**Tools & Methods:**
- UniProt REST API → programmatic FASTA retrieval
- NCBI blastp via `Bio.Blast.NCBIWWW.qblast()` (Biopython 1.85)
- Database: `refseq_protein` | Filter: `Mammalia[Organism]` | 15 hits per query
- Results parsed from XML → CSV + bar charts (Matplotlib)

**Key Results:**

| Protein | Mean Identity | Min | Max | Hits at 100% |
|---------|--------------|-----|-----|--------------|
| p53 (TP53) | **98.0%** | 95.7% | 100% | 2/15 |
| KRAS (WT)  | **99.7%** | 99.5% | 100% | 6/15 |

> **Key insight:** KRAS is significantly more conserved than p53 across Mammalia. Glycine at position 12 (G12) — the G12D mutation hotspot — has been under extreme purifying selection for ~450 million years of vertebrate evolution, because any substitution impairs GTPase function.

[![Open in Jupyter](https://img.shields.io/badge/Open-Jupyter%20Notebook-F37626?style=flat-square&logo=jupyter)](Task1_BLAST/KRAS_Task1_BLAST.ipynb)

---

## 🧬 Task 2 — Multiple Sequence Alignment (MSA)

**Objective:** Align KRAS protein sequences from 5 vertebrate species using Clustal Omega, quantify per-position conservation, and demonstrate why G12 is an oncogenic hotspot.

**Species selected:**

| # | Species | Common name | UniProt | Length | Role |
|---|---------|-------------|---------|--------|------|
| 1 | *Homo sapiens* | Human | P01116 | 189 aa | Reference |
| 2 | *Mus musculus* | Mouse | P32883 | 189 aa | Cancer model |
| 3 | *Rattus norvegicus* | Rat | Q05144 | 192 aa | Oncology model |
| 4 | *Macaca mulatta* | Rhesus macaque | F7H3J8 | 290 aa | Primate outgroup |
| 5 | *Danio rerio* | Zebrafish | Q6NYN2 | 321 aa | Distant outgroup |

**Tools & Methods:**
- Clustal Omega via EBI REST API (`https://www.ebi.ac.uk/Tools/services/rest/clustalo`)
- Alignment: 429 positions | Job ID: `clustalo-R20260520-122300-0184-43298910-p2m`
- Per-position conservation scores computed via `Bio.AlignIO`
- G12D mutation computationally simulated on the human reference sequence

**Key Results:**
- Human–Mouse and Human–Rat identity: **98.9%**
- G12 (Glycine, position 12): **100% conserved** in canonical mammalian sequences
- G12D simulation: Glycine (57 Da, tiny) → Aspartic Acid (115 Da, charged) = GAP blocked → KRAS constitutively active

[![Open in Jupyter](https://img.shields.io/badge/Open-Jupyter%20Notebook-F37626?style=flat-square&logo=jupyter)](Task2_MSA/KRAS_Task2_MSA.ipynb)

---

## 💊 Task 3 — Literature Review: Role of Bioinformatics in Drug Discovery

**Objective:** 6-page literature review demonstrating how bioinformatics made KRAS G12D — previously undruggable for 40 years — into a validated clinical target.

**Topics covered:**
1. The modern drug discovery pipeline and computational contributions
2. Sequence analysis & target identification (BLAST, MSA, UniProt)
3. Structural bioinformatics & AlphaFold (Nobel Prize 2024)
4. Virtual screening & molecular docking (AutoDock, GNINA)
5. Molecular dynamics simulations & free energy landscapes
6. Machine learning in drug discovery (DeepPurpose, GNINA CNN)

**KRAS G12D Clinical Case Study:**

| Inhibitor | Mechanism | State | Status | Key Data |
|-----------|-----------|-------|--------|----------|
| MRTX1133 | Non-covalent, S-IIP | GDP-bound | Terminated Q1 2025 (BMS) | IC50 < 2 nM, 700× selectivity |
| Zoldonrasib (RMC-9805) | Covalent RAS-ON, CypA tri-complex | GTP-bound (active) | Phase I/1b active (NCT06040541) | **30% ORR, 80% DCR** in PDAC (2024) |

> **Landmark result:** Zoldonrasib achieved 30% Objective Response Rate and 80% Disease Control Rate in KRAS G12D-mutant pancreatic cancer patients (EORTC-NCI-AACR, Barcelona, October 2024) — a historic breakthrough for one of the deadliest cancers.

---

## ⚙️ Setup & Reproduction

### Requirements
```bash
pip install biopython requests matplotlib numpy pandas
```

### Run Task 1
```bash
# Open in JupyterLab or Jupyter Notebook
jupyter notebook Task1_BLAST/KRAS_Task1_BLAST.ipynb
```
> ⚠️ BLAST queries via NCBI web API take 2–5 minutes each. Do not interrupt the cells.

### Run Task 2
```bash
jupyter notebook Task2_MSA/KRAS_Task2_MSA.ipynb
```
> ⚠️ Clustal Omega EBI submission takes ~60 seconds. Requires internet connection.

### Environment tested on
- Python 3.9 | Biopython 1.85 | Anaconda JupyterHub (anaconda-2022.05-py39)
- NCBI blastp | EBI Clustal Omega REST API

---

## 📚 Key References

1. Zeissig MN, et al. (2023). Targeting cancers with KRAS-G12D mutations. *Trends Cancer*, 9(11):955-67. https://pubmed.ncbi.nlm.nih.gov/37591766/
2. Kondo Y, et al. (2023). Switch II pocket of KRAS(G12D) with monobody inhibitors. *PNAS*, 120(28):e2302485120. https://www.pnas.org/doi/10.1073/pnas.2302485120
3. Wei D, et al. (2024). MRTX1133 targets KRAS G12D in PDAC. *Clin Cancer Res*, 30(4):655-662. https://pubmed.ncbi.nlm.nih.gov/37831007/
4. Papadopoulos KP, et al. (2025). Zoldonrasib (RMC-9805) Phase I in PDAC. *J Clin Oncol*, 43(4_suppl):724. https://ascopubs.org/doi/10.1200/JCO.2025.43.4_suppl.724
5. Jumper J, et al. (2021). AlphaFold. *Nature*, 596:583-589. [2024 Nobel Prize in Chemistry] https://www.nature.com/articles/s41586-021-03819-2
6. Sievers F, et al. (2011). Clustal Omega. *Mol Syst Biol*, 7:539. https://pubmed.ncbi.nlm.nih.gov/21988835/
7. UniProt Consortium. (2023). UniProt in 2023. *Nucleic Acids Res*, 51(D1):D523. https://academic.oup.com/nar/article/51/D1/D523/6835362

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🤝 Connect

**Charles Arnaud Jesutin Hounsou-Kan**  
Medical Biotechnology Graduate | Aspiring PhD Researcher in Computational Oncology

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square&logo=linkedin)](https://linkedin.com/in/your-profile)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat-square&logo=github)](https://github.com/your-username)
[![Email](https://img.shields.io/badge/Email-Contact-D85A30?style=flat-square&logo=gmail)](mailto:charleshounsoukan@gmail.com)

---

*Independent research project, May–June 2026.*
