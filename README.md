# RNA-seq Analysis on Raspberry Pi

## Overview
This repository provides a step-by-step guide for performing RNA-seq analysis locally on a Raspberry Pi using a USB SSD for storage. The workflow demonstrates how standard RNA-seq pipelines can be adapted to run on low-power, edge computing hardware without reliance on cloud infrastructure.

The pipeline includes:
- Downloading sequencing data from NCBI SRA
- Quality control (FastQC)
- Read processing (Trimmomatic)
- Transcript quantification (Kallisto)
- Local data management and visualization

---

## Key Features
- Fully local RNA-seq pipeline (no cloud required)
- Designed for Raspberry Pi (ARM architecture)
- External USB SSD storage for large datasets
- Apache2 integration for browser-based access
- Optional JupyterLab interface

---

## Original Work (Attribution)

This project is adapted from the following teaching resource:

**Williams J. et al. (2019)**  
*RNA-Seq analysis of Mouse Leptin Gene*  
Genomics Education Alliance  

Available at:  
https://cyverse-leptin-rna-seq-lesson-dev.readthedocs-hosted.com/en/latest/index.html

The original workflow uses CyVerse cloud infrastructure for data storage and computation.

---

## Key Differences from Original Workflow

| Feature        | CyVerse Lesson (Original) | This Project |
|----------------|--------------------------|--------------|
| Compute        | Cloud (CyVerse JupyterLab) | Local Raspberry Pi |
| Storage        | CyVerse Data Store         | USB SSD |
| Execution      | Remote                     | Fully local |
| Setup          | Pre-configured             | Manual installation |
| Scalability    | High-performance cluster   | Low-power device |

---

## System Architecture
