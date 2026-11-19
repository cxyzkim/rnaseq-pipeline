# 🧬 RNAseq Pipeline using Bowtie2

This pipeline processes RNA-seq data using **Bowtie2**.  
Supports **mouse (Mus musculus) and human (Homo sapiens) genomes**.


## 📖 **Need a step-by-step tutorial?**  
For a detailed explanation and practical walkthrough, please refer to the following Notion page:  
👉 [RNA-seq with Bowtie2 – Full Tutorial](https://lapis-stilton-259.notion.site/RNA-seq-with-Bowtie2-1c337172436b80afa409d1a9f165e313?pvs=4)

## 📥 Installation 

Before running this pipeline, ensure that the following programs are installed:

### 🔹 Required Dependencies
- **Bowtie2**: `bowtie2-build` & `bowtie2`
- **Samtools**: `samtools`
- **FeatureCounts** (from `subread` package)
- **FastQC** & **MultiQC** (for quality control)
- **R(dplyr)**: Required for merging counts (`merge_output.R`)

All of these can be installed with the provided conda environment:
```bash
conda env create -f RNAseq.yaml && conda activate RNAseq
```

---

## 🚀 How to Use 

### 1️⃣ Download the pipeline
Clone this repository:
```bash
git clone https://github.com/cxyzkim/rnaseq-pipeline.git
```

### 2️⃣ Set up your working directory
Create a separate working space and prepare your input files:
```bash
mkdir working_space
cd working_space

mkdir input ref
mv your_fastq_files input/
mv your_reference_files ref/
cp -r ../rnaseq-pipeline/command . 
```
📌 **This ensures that all input and reference files are placed in the correct directories.**  
📌 **The scripts from `rnaseq-pipeline/command` are copied to the working directory for execution.**

Expected file names:
- FASTQ: `input/<sample_name>_1.fq.gz` and `input/<sample_name>_2.fq.gz` (paired-end)
- Reference: `ref/<reference>.fa` (genome FASTA) and `ref/<reference>.gtf.gz` (gzipped GTF), e.g. `ref/mm10.fa`, `ref/mm10.gtf.gz`
- `<reference>` must start with `mm` (mouse) or `hg` (human)
- The Bowtie2 index (`ref/<reference>.*.bt2`) is built automatically on the first run if missing

### 3️⃣ Prepare your metadata file
Create a sample metadata file inside the `input/` directory:
```bash
echo -e "sample1 5 mm10\nsample2 3 hg38" > input/input_file.txt
```
📌 **Format**: `<sample_name> <threads> <reference>`

---

### 4️⃣ Run the pipeline
To start the RNAseq analysis, execute:
```bash
bash command/main_bowtie2.sh
```
The script asks for the metadata file name interactively. Enter only the file name inside `input/` (e.g. `input_file.txt`, not `input/input_file.txt`).

This will:
1. Check for required files
2. Create necessary directories
3. Run Bowtie2 alignment
4. Filter and preprocess BAM files
5. Count mapped reads using featureCounts
6. Merge final results into a single CSV file

### 5️⃣ Outputs
- `output/<sample_name>_counts.csv`: read counts per gene for each sample
- `output/raw_counts.csv`: merged count table (genes × samples), inner join on gene ID
- `work/<sample_name>/`: intermediate BAM files and featureCounts output
- `work/<sample_name>/QC/`: FastQC and MultiQC reports

📌 The merge step (`merge_output.R`) expects at least two samples in the metadata file.

---

## 👨‍💻 Author
Developed by **[Chaeyeon Kim]**  
GitHub: [cxyzkim](https://github.com/cxyzkim/)
