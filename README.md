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

If you encounter any problem with the default settings, we recommend use the [environment.yml](https://github.com/Gaoyuan-Li/BENG183_HW3_2023Fall/blob/main/environment.yml) (tested in ubuntu 22.04) in the repository to install the environment.

```bash
conda env create -f environment.yml
```

Please change the prefix to your own path.

###### 1.2 Sequencing files

Please download the sequencing files from the following link: https://drive.google.com/file/d/12qNoEYrJk6xbInxLHX3jOZXimvWLVSB6/view?usp=sharing

Or download  from this github repository [data_chrX ](https://github.com/Gaoyuan-Li/BENG183_HW3_2023Fall/tree/main/data_chrX)(Note: each file was compressed due to the 100MB limitation in github repository. Please download each of the .gz files and put them in the same folder named data_chrX)

#### 2. Quality Control with FastQC

###### 2.1 **Why Quality Control is Crucial for RNA-seq Data**

Before processing and analyzing RNA-seq data, it's essential to assess its quality. High-quality data will lead to more accurate downstream analyses, whereas low-quality data can introduce biases and inaccuracies. Quality control (QC) helps identify issues such as sequencing errors, contamination, and biases, allowing for informed decisions on further data processing steps.

###### 2.2 **Running FastQC on Raw Sequencing Data**

```bash
mkdir fastqc

fastqc -o fastqc/ -t 16 data_chrX/ERR188044_chrX_1.fastq
```

- `fastqc`: Calls the FastQC program.
- `-o fastqc/`: Specifies the output directory where FastQC will save its results. In this case, it's a directory named "fastqc."
- `-t 16`: Tells FastQC to use 16 threads for the analysis, speeding up the process.
- `data_chrX/ERR188044_chrX_1.fastq`: Specifies the input file, which is a FASTQ file containing the raw sequencing reads.

###### 2.3 **Interpreting FastQC Reports**

After running FastQC, you'll get a `.html` report that provides various metrics and visualizations to assess the quality of your RNA-seq data:

1. **Basic Statistics**: Provides general information about the dataset, like the total number of sequences, sequence length, and the overall assessment of data quality.
2. **Per Base Sequence Quality**: Displays the quality scores across all bases at each position in the reads. Ideally, most of the plot should be in the green region. Yellow or red regions suggest poor quality.
3. **Per Tile Sequence Quality**: If using Illumina sequencing, this checks for tile-specific issues. Variations might indicate a problem during sequencing.
4. **Per Sequence Quality Scores**: Shows the distribution of average quality scores per read. A left-skewed distribution (towards higher quality scores) is desirable.
5. **Per Base Sequence Content**: Checks if the proportion of each base (A, T, C, G) changes over the length of the reads. Consistent base proportions are expected unless there's a known reason for variation.
6. **Per Sequence GC Content**: Compares the GC content distribution in your reads to a theoretical distribution. A significant deviation might indicate contamination or a biased library.
7. **Per Base N Content**: Reports the percentage of bases at each position for which a base could not be determined.
8. **Sequence Length Distribution**: Indicates the range of sequence lengths in the dataset.
9. **Sequence Duplication Levels**: Reports the relative level of duplication for every sequence in the set.
10. **Overrepresented Sequences**: Lists sequences that appear more often than expected.
11. **Adapter Content**: Checks for the presence of adapter sequences, which can occur when the insert is shorter than the read length.

#### 3. Reads Trimming and Filtering with Fastp

```
fastp -i data_chrX/ERR188044_chrX_1.fastq -I data_chrX/ERR188044_chrX_2.fastq -o data_chrX/ERR188044_chrX_1_clean.fastq -O data_chrX/ERR188044_chrX_2_clean.fastq
```



#### 4. Aligning Reads to the Reference Genome with STAR

```
# check if STAR has been successfully installed.
STAR -h 

# build index
STAR --runThreadN 16 --runMode genomeGenerate --genomeDir chrX_STAR_index/ --genomeFastaFiles data_chrX/chrX.fa --sjdbGTFfile data_chrX/chrX.gtf --sjdbOverhang 100
```



```
# Reads mapping

STAR --runThreadN 16 --genomeDir chrX_STAR_index/ --readFilesIn data_chrX/ERR188044_chrX_1_clean.fastq data_chrX/ERR188044_chrX_2_clean.fastq --outSAMtype BAM SortedByCoordinate --outFileNamePrefix ./ERR188044_BAM/ERR188044_STAR_
```



#### 5. Gene Expression Quantification with FeatureCounts

```
mkdir featureCounts

featureCounts -p -a data_chrX/chrX.gtf -T 16 -o featureCounts/ERR188044_counts.txt ERR188044_BAM/ERR188044_STAR_Aligned.sortedByCoord.out.bam
```



#### 6. Differentially expressed genes (BONUS)

```

```

