# docs/ – File Descriptions
------------------------------------------------------------------------

```
installation.md
```
**Purpose:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Step-by-step setup of the Raspberry Pi software environment.

**Contains:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;System update and package installation

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Conda / environment setup

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Installation of SRA Toolkit, FastQC, Kallisto

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional JupyterLab setup

**Goal:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get a fresh Raspberry Pi ready to run RNA-seq workflows

------------------------------------------------------------------------

```
storage-setup.md
```
**Purpose:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Configuration of external USB SSD for RNA-seq data storage.

**Contains:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Disk identification and formatting

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mounting to /var/www/html/usb

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Permission configuration (pi + www-data)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Auto-mount setup (fstab)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Storage architecture explanation (SD vs SSD)

**Goal:** 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ensure reliable, high-capacity storage for sequencing data

------------------------------------------------------------------------

```
pipeline.md
```
**Purpose:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Core RNA-seq workflow executed on the Raspberry Pi.

**Contains:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SRA download (prefetch)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FASTQ conversion (fasterq-dump)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Compression and QC (FastQC)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional trimming (Trimmomatic)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Quantification (Kallisto)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Output structure and interpretation

**Goal:** 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Provide a reproducible RNA-seq analysis pipeline

------------------------------------------------------------------------

```
apache-jupyter.md
```

**Purpose:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Configuration of web-based access and interactive analysis tools.

**Contains:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Apache2 setup and module configuration

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reverse proxy configuration for JupyterLab

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Accessing data via browser

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Running JupyterLab locally

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Basic security considerations

**Goal:** 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Enable browser-based interaction with data and analysis

------------------------------------------------------------------------

```
original-work.md
```

**Purpose:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Formal attribution and context for the source material.

**Contains:**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reference to CyVerse RNA-seq lesson

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Summary of original workflow

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Description of cloud-based implementation

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Clear statement of how this project differs

**Goal:** 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ensure proper credit and academic transparency
