## 1. Overview
While massive sequence databases have recently revolutionized computational protein structure prediction, RNA research has historically lagged due to a lack of consolidated sequence resources. The **elDORS** database bridges this critical gap. By strategically integrating  genomic and metagenomic databases, **elDORS_v1_raw** (the raw, foundational tier of our version 1 release) provides a massive-scale, up-to-date repository of RNA sequence data. Here, we also provide an 80% sequence-identity (considering 80% sequence overlap) clustered version **elDORS_v1** (explicitly designed for efficient use with advanced bioinformatics pipelines).
Our benchmarking demonstrates that elDORS-augmented pipelines match or exceed the alignment depth of massive legacy databases, effectively eliminating the sequence retrieval failures that typically challenge "orphan" RNAs.
To bypass the severe network timeouts and I/O bottlenecks associated with transferring monolithic files, the **3.2 TB** elDORS dataset is distributed in precisely engineered, multi-volume architectures. These distributions are optimized for high-speed parallel downloads and immediate drop-in compatibility with leading multiple sequence alignment (MSA) pipelines.

Note: The elDORS database is distributed under the CC-BY 4.0 license

---

## 2. Dataset Architecture & Distributions

The total size of the directory is ~3.2 TB. It is divided into four primary **Distributions** and **Pipeline Builds** to suit different computational environments and workflows.

### Summary Table

| Distribution / Pipeline Build | Path / Directory | Size | Description |
| :--- | :--- | :--- | :--- |
| **Unclustered database** | `./elDORS_v1_raw` | 1.2 TB | Raw (unclustered) database version (elDORS_v1_raw) |
| **Clustered version** | `./elDORS_v1` | 170 GB | 80% sequence-identity (considering 80% overlap) clustered version (elDORS_v1) |
| **rMSA-Optimized Build** | `./rMSA_optimized_elDORS` | ~ 1.0 TB | Optimized elDORS_V1 for rMSA pipeline |
| **RNAcmap3-Optimized Build** | `./RNAcmap3_optimized_elDORS` | 861 GB | Optimized elDORS_V1 for RNAcmap3 split-strategy pipeline |

### Directory Structure
```text
elDORS_v1_Database/
├── elDORS_v1_raw/                 (1.2 TB)  - Raw (unclustered) multi-volume FASTA format sequence database (provide as sequence-aware ~9GB compressed (fasta.gz) chunks)
├── elDORS_v1/                    - elDORS_v1 (80% sequence identity clustered (with 80% overlap) version)
│  └── elDORS_v1_chunks/          (170 GB)  - Multi-volume FASTA format database provided as sequence-aware ~9GB compressed (fasta.gz) chunks 
├── rMSA_optimized_elDORS/           (1022 GB) - Optimized elDORS_V1 for rMSA pipeline: uncompressed FASTA format elDORS_v1 along with multi-volume BLAST format files 
└── RNAcmap3_optimized_elDORS/       (861 GB)  - Optimized elDORS_V1 for RNAcmap3 split-strategy pipeline
    ├── blast/                     (286 GB)  - Multi-volume BLAST format database optimized for RNAcmap3 pipeline
    └── infernal/                  (575 GB)  - Uncompressed FASTA format elDORS_v1 (multiple volumes) compatible with RNAcmap3 pipeline
```
#### 1. Database Curation & Redundancy Removal Pipeline
The elDORS database is built by integrating vast genomic, non-coding RNA (ncRNA), and metagenomic resources. To make this resource computationally efficient, we applied a strict hierarchical redundancy removal and an 80% sequence identity (considering 80% sequence overlap) clustering workflow:

![elDORS Curation Pipeline](images/elDORS_creation_workflow.jpg)

#### 2. Downstream Optimization for MSA generation pipelines
To enable immediate drop-in compatibility, the dataset is provided in specialized, pre-indexed builds optimized for cutting-edge RNA multiple sequence alignment (MSA) and contact prediction tools like `rMSA` and `RNAcmap3`, and also precisely curated to ensure efficient downstream use, such as RNA language model training using either the sequences from the database or the Multiple sequence alignments generated using the database:

![elDORS Downstream Pipelines](images/elDORS_downstream_application.jpg)

### 3. Data Sources & Citation

The elDORS database is constructed by comprehensively integrating a vast array of genomic, non-coding RNA, and metagenomic resources. A complete, tabulated breakdown of all primary data sources and our curation methodology is available in our preprint. 

If you use the elDORS database or our optimized pipeline builds in your research, please cite:

> **Dutta, N., & Vicens, Q. (2026). elDORS: An elevated Database Of RNA Sequences.** *bioRxiv*. [https://www.biorxiv.org/content/10.64898/2026.07.10.737016v1](https://www.biorxiv.org/content/10.64898/2026.07.10.737016v1)

**Additionally, please support the resources that make this work possible:**
 When utilizing sequences from this database, we strongly encourage users to also cite the component source databases and repositories. A comprehensive list of references for these foundational resources is provided in the "Methods" section of our preprint.
