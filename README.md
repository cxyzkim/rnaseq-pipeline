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

---

## 🚀 How to Use 

### 1️⃣ Download the pipeline
Clone this repository:
```bash
git clone https://github.com/cykim-saihst/rnaseq-pipeline.git
```

### 2️⃣ Set up your working directory
Create a separate working space and prepare your input files:
```bash
mkdir working_space
cd working_space

mkdir input ref
mv your_fastq_files input/
mv your_reference_files ref/
cp -r ../RNAseq_pipeline/command . 
```
📌 **This ensures that all input and reference files are placed in the correct directories.**  
📌 **The scripts from `RNAseq_pipeline/command` are copied to the working directory for execution.**

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
This will:
1. Check for required files
2. Create necessary directories
3. Run Bowtie2 alignment
4. Filter and preprocess BAM files
5. Count mapped reads using featureCounts
6. Merge final results into a single CSV file

---

## 📌 Example Workflow
```bash
git clone https://github.com/cykim-saihst/rnaseq-pipeline.git

mkdir working_space
cd working_space

mkdir input ref
mv your_fastq_files input/
mv your_reference_files ref/
cp -r ../RNAseq_pipeline/command . 

echo -e "sample1 5 mm10\nsample2 3 hg38" > input/input_file.txt
bash command/main_bowtie2.sh
```

---

## 👨‍💻 Author
Developed by **[Chaeyeon Kim]**  
GitHub: [cykim-saihst](https://github.com/cykim-saihst/)
