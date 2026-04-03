# RNA-seq Analysis on Raspberry Pi

![Platform](https://img.shields.io/badge/platform-Raspberry%20Pi-red)
![Language](https://img.shields.io/badge/python-3.10-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active%20development-brightgreen)

RNA-seq Analysis on Raspberry Pi is an open-source bioinformatics
platform for performing RNA sequencing analysis locally on a Raspberry
Pi using external USB SSD storage.

The system enables fully local processing of RNA-seq datasets, including
data download, quality control, and transcript quantification, without
reliance on cloud-based infrastructure.

Designed to be low-cost, reproducible, and extensible, the platform
demonstrates how standard RNA-seq workflows can be adapted for edge
computing environments using commodity hardware and open-source tools.

------------------------------------------------------------------------

# Overview

RNA sequencing (RNA-seq) is a widely used technique for analysing gene
expression, but typical workflows rely on high-performance computing
clusters or cloud-based platforms.

This project provides a local-first alternative by enabling RNA-seq
analysis on a Raspberry Pi, allowing users to:

-   download sequencing data directly from NCBI SRA
-   perform quality control (FastQC)
-   optionally trim reads (Trimmomatic)
-   quantify transcript abundance (Kallisto)
-   store and manage data locally on USB SSD
-   access results via a browser-based interface (Apache2 / Jupyter)

The system is intended for research, teaching, and prototyping
environments where low-cost and reproducible bioinformatics workflows are
valuable.

------------------------------------------------------------------------

# Key Features

-   Fully local RNA-seq pipeline (no cloud required)
-   Raspberry Pi compatible (ARM architecture)
-   USB SSD storage for large sequencing datasets
-   Integration with SRA Toolkit (prefetch, fasterq-dump)
-   Quality control with FastQC
-   Transcript quantification using Kallisto
-   Optional read trimming with Trimmomatic
-   Apache2 integration for browser-based data access
-   Optional JupyterLab interface for interactive analysis
-   Reproducible and modular workflow design

------------------------------------------------------------------------

# System Architecture

The platform consists of four main components:

1.  Data acquisition (NCBI SRA)
2.  Raspberry Pi compute environment
3.  External USB SSD storage
4.  Web-based access interface

Typical architecture:
```
NCBI SRA → Raspberry Pi → USB SSD → Bioinformatics Tools → Results  
→ Apache2 / JupyterLab → Browser Access
```
------------------------------------------------------------------------

# Original Work and Attribution

This project is adapted from the following teaching resource:

Williams J. et al. (2019)  
RNA-Seq analysis of Mouse Leptin Gene  
Genomics Education Alliance  

Available at:  
https://cyverse-leptin-rna-seq-lesson-dev.readthedocs-hosted.com

The original workflow uses CyVerse cloud infrastructure for data storage
and computation.

This repository reimplements the workflow for local execution on
Raspberry Pi hardware.

------------------------------------------------------------------------

# Key Differences from Original Workflow
```
  Feature        CyVerse Lesson (Original)   This Project
  -------------- --------------------------- ---------------------------
  Compute        Cloud (CyVerse JupyterLab)  Local Raspberry Pi
  Storage        CyVerse Data Store          USB SSD
  Execution      Remote                      Fully local
  Setup          Pre-configured              Manual installation
  Scalability    HPC infrastructure          Low-power device
```
------------------------------------------------------------------------

# Example Applications

Possible use cases include:

-   RNA-seq teaching and training environments
-   prototyping bioinformatics pipelines
-   edge-based genomics workflows
-   low-cost laboratory computational setups
-   offline or data-sovereign analysis environments
-   reproducible research demonstrations

------------------------------------------------------------------------

# Hardware Requirements

Minimum tested configuration:
```
  Component               Example
  ----------------------- ---------------------------------------
  Single-board computer   Raspberry Pi 4 or Raspberry Pi 5
  Storage                 USB SSD (≥ 500 GB recommended)
  System disk             microSD card (32–128 GB)
  Network                 Ethernet or WiFi
  Power                   5V / 3A power supply
```
Optional hardware:

-   powered USB hub (for stability)
-   cooling (heatsink or fan)
-   UPS (for long-running jobs)

Detailed setup instructions:
```
docs/storage-setup.md
```
------------------------------------------------------------------------

# Software Requirements

Required software components:

-   Raspberry Pi OS (Debian-based)
-   Python 3.10+
-   SRA Toolkit (prefetch, fasterq-dump)
-   FastQC
-   Trimmomatic (optional)
-   Kallisto
-   Apache2 web server
-   Optional JupyterLab

Installation instructions:
```
docs/installation.md
```
------------------------------------------------------------------------

# Quick Start

Clone the repository:
```
git clone https://github.com/richardmorgan1530/rna-seq-raspberry-pi.git
cd rna-seq-raspberry-pi
```
Install dependencies:
```
bash scripts/install.sh
```
Run example pipeline:
```
bash scripts/run_pipeline.sh
```
Access results:
```
http://<raspberry-pi-ip>/usb/
```
Detailed pipeline instructions:
```
docs/pipeline.md
```
------------------------------------------------------------------------

# Data Access and Web Interface

The system provides browser-based access to data via Apache2:
```
http://<raspberry-pi-ip>/usb/
```
Optional JupyterLab integration enables interactive analysis:
```
http://<raspberry-pi-ip>/jupyter/
```

Configuration details:
```
docs/apache-jupyter.md
```
------------------------------------------------------------------------

# Performance Considerations

This platform is not inherently limited by dataset size, but is constrained by available compute resources (CPU, RAM, and I/O throughput). As a result, larger RNA-seq datasets can be processed, but with increased runtime.

Typical characteristics:
```
  Parameter                   Expected Performance
  --------------------------- -----------------------
  CPU performance             Limited (ARM-based)
  RAM                         4–8 GB
  Processing time             Slower than HPC systems
  Storage performance         Dependent on USB SSD speed
```
## Storage Architecture

The system uses a dual-storage setup:

-   **microSD card (e.g. 32 GB)** → Operating system and core software  
-   **USB SSD (e.g. 1 TB or larger)** → RNA-seq data, FASTQ files, intermediate outputs, and results  

This separation is essential to:
-   avoid excessive wear on the SD card  
-   prevent storage limitations during dataset download and processing  
-   improve I/O performance  

Due to the large size of RNA-seq datasets, even a single FASTQ file may exceed the practical capacity of the SD card.  
All sequencing data should therefore be stored and processed on the USB SSD.

## Storage Scalability

The USB SSD capacity can be scaled depending on requirements:

-   larger datasets can be supported with higher-capacity drives  
-   powered USB hubs may be required for stable operation of high-capacity SSDs  
-   storage expansion is limited primarily by power delivery and USB interface constraints  

## Performance Recommendations

For optimal performance:

-   store all sequencing data and outputs on the USB SSD  
-   avoid running RNA-seq workflows on the SD card  
-   limit thread usage to match available CPU cores  
-   use compressed FASTQ files where possible  
-   process small to moderate datasets  

## Notes

-   RNA-seq workflows are both CPU- and I/O-intensive  
-   performance will vary depending on SSD speed and USB interface  
-   long-running jobs may require active cooling for stability  

------------------------------------------------------------------------

# Reproducibility

This project aims to provide a fully reproducible RNA-seq workflow.

The repository includes:

-   installation instructions
-   standardised pipeline steps
-   documented system configuration
-   modular workflow components

Full documentation:
```
docs/
```
------------------------------------------------------------------------

# Limitations

This platform is intended for research and educational use only.

Limitations include:

-   limited computational power
-   long processing times for large datasets
-   not suitable for large-scale RNA-seq studies
-   dependency on stable power and storage

Users should ensure appropriate validation before research use.

------------------------------------------------------------------------

# Project Structure
```
rna-seq-raspberry-pi
│
├── README.md
├── LICENSE
│
├── docs
│ ├── installation.md
│ ├── storage-setup.md
│ ├── pipeline.md
│ ├── apache-jupyter.md
│ └── original-work.md
│
├── scripts
│ ├── install.sh
│ └── run_pipeline.sh
│
├── config
│ └── README.md
│
└── data
```
------------------------------------------------------------------------

# Contributing

Contributions are welcome.

Potential areas for development include:

-   pipeline automation
-   performance optimisation
-   GPU or accelerator integration
-   improved visualisation tools
-   multi-sample batch processing
-   downstream analysis integration (DESeq2, edgeR)

Please see:
```
CONTRIBUTING.md
```
------------------------------------------------------------------------

# Citation

If you use this project in research or teaching, please cite it.

Example citation:
```
Morgan R. RNA-seq Analysis on Raspberry Pi: an edge-based
bioinformatics workflow. GitHub repository.
```
------------------------------------------------------------------------

# License

This project is released under the MIT License.

See:
```
LICENSE
```
------------------------------------------------------------------------

# Contact

Project maintainer:
```
Richard Morgan  
MSc Regenerative Medicine  
University of Galway
```
