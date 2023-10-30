# BENG183 HW3 Tutorial
#### Introduction

Welcome to this tutorial on executing an RNA-seq analysis pipeline. RNA-sequencing (RNA-seq) has revolutionized our ability to analyze gene expression profiles in a high-throughput manner. This tutorial is designed to guide you step by step through the processes of quality control, alignment, and quantification of RNA-seq data using popular bioinformatics tools.

#### Objectives

By the end of this tutorial, you should be able to:

1. Understand the importance of each step in the RNA-seq analysis pipeline.
2. Perform quality control checks on raw sequencing data using FastQC.
3. Trim and filter raw sequencing reads using Fastp.
4. Align the processed reads to a reference genome using STAR.
5. Quantify gene expression levels using FeatureCounts.

#### Outline

1. **Setting up the environment:**
   - Installing and setting up necessary tools
2. **Quality Control with FastQC:**
   - Running FastQC on raw sequencing data
   - Interpreting FastQC reports
3. **Reads Trimming and Filtering with Fastp:**
   - Running Fastp to clean up raw sequencing data
   - Verifying the quality of trimmed reads with FastQC
4. **Aligning Reads to the Reference Genome with STAR:**
   - Setting up the reference genome
   - Running STAR for aligning RNA-seq reads
   - Interpreting the STAR alignment summary
5. **Gene Expression Quantification with FeatureCounts:**
   - Running FeatureCounts to quantify gene expression levels
   - Interpreting the output of FeatureCounts
6. **Differentially expressed genes (BONUS):**
   - Using DESeq2 to identify the differentially expressed genes (DEGs)

## **Let's begin!**

#### 1. Setting up the environment and downloading data

###### 1.1 Conda environment

```bash
# create a new environment

conda create -n beng183

# install all required packages

conda install -c bioconda fastqc
conda install -c bioconda fastp
conda install -c bioconda star
conda install -c bioconda samtools
conda install -c bioconda subread
```

We do not specify any version here to let conda select the compatible version

If you encounter any problem with the default settings, we recommend use the 

[environment.yml]: https://github.com/Gaoyuan-Li/BENG183_HW3_2023Fall/blob/main/environment.yml

 (tested in ubuntu 22.04) in the repository to install the environment.

```bash
conda env create -f environment.yml
```

Please change the prefix to your own path.

###### 1.2 Sequencing files

Please download the sequencing files from the following link: https://drive.google.com/file/d/1EVAC8fx8-CmKqS_NyqOtDIqKtUev95CG/view?usp=sharing

Or from this github repository (./data_chrX):

https://github.com/Gaoyuan-Li/BENG183_HW3_2023Fall/tree/main/data_chrX

#### 2. Quality Control with FastQC

```

```



#### 3. Reads Trimming and Filtering with Fastp

```

```



#### 4. Aligning Reads to the Reference Genome with STAR

```

```



#### 5. Gene Expression Quantification with FeatureCounts

```

```



#### 6. Differentially expressed genes (BONUS)

```

```

