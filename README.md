# Gene-Expression-Analysis_IB
This repository provides a beginner-friendly guide to gene expression analysis using transcriptomics data. It explains the biological background, major technologies such as microarrays and RNA-seq, and the main computational steps used to analyse large-scale gene expression datasets.
# Gene Expression Analysis: Transcriptomics and Big Data

## Repository Description

This repository provides a beginner-friendly guide to gene expression analysis using transcriptomics data. It explains the biological background, major technologies such as microarrays and RNA-seq, and the main computational steps used to analyse large-scale gene expression datasets.

The repository is based on lecture notes covering:

- Transcriptomics technologies
- RNA-seq and microarray workflows
- Differential gene expression analysis
- Pathway and ontology analysis
- Clustering and heatmaps
- Single-cell RNA-seq concepts
- Biological interpretation of gene expression data

---

## Repository Aim

The aim of this repository is to understand how gene expression data can be collected, processed, analysed, and interpreted to study biological systems.

By the end of this repository, a reader should understand:

- What the transcriptome is
- Why RNA is studied in gene expression analysis
- How RNA-seq and microarrays measure gene expression
- How differentially expressed genes are identified
- How volcano plots, heatmaps, and clustering are used
- How pathway analysis gives biological meaning to gene lists

---

1. Introduction to Gene Expression

Gene expression is the process by which information stored in DNA is used to make RNA and proteins.

The basic flow of biological information is:

DNA → RNA → Protein

This is known as the central dogma of molecular biology.

Gene expression analysis focuses mainly on RNA because RNA shows which genes are active in a cell at a particular time or condition.

---

## 2. What is the Transcriptome?

The transcriptome is the complete set of RNA transcripts produced inside a cell under a specific condition.

It includes:

## Types of RNA

| RNA Type | Description |
|-----------|-------------|
| **mRNA (Messenger RNA)** | Carries genetic information from DNA to ribosomes for protein synthesis. |
| **rRNA (Ribosomal RNA)** | Structural and functional component of ribosomes involved in protein synthesis. |
| **tRNA (Transfer RNA)** | Transfers amino acids to ribosomes during protein synthesis. |
| **lncRNA (Long Non-coding RNA)** | Long RNA molecules that do not code for proteins but regulate gene expression and cellular processes. |
| **microRNA (miRNA)** | Small non-coding RNA molecules involved in post-transcriptional gene regulation by targeting mRNA. |

Different cells can have the same genome but different transcriptomes

For example:

Neuron cell ≠ Muscle cell ≠ Stem cell


Even though they share almost the same DNA, they express different genes.

---

## 3. Why Study RNA?

RNA gives information about gene activity.

A gene may exist in DNA, but it may not always be active. If a cell needs a gene, it produces RNA copies of that gene.

More RNA copies usually mean higher gene expression.

Example
```text
High mRNA count = gene is highly active
Low mRNA count = gene is weakly active
No mRNA count = gene may be inactive
```

---

## 4. Gene Expression Data Type

Gene expression data is usually count-based or continuous.

Example

```
Gene A = 500 reads
Gene B = 20 reads
Gene C = 0 reads
```

This is different from DNA variant data, which is often categorical.

Example

```
Wild type / mutant
Homozygous / heterozygous
Present / absent
```

Because gene expression data is numerical, it requires statistical analysis.

## 5. Technologies for Measuring Gene Expression

### 5.1 Low-throughput Methods


These measure one or a few genes at a 
time

RNA Detection and Expression Analysis Methods

| Method | Purpose |
|----------|---------|
| **Northern Blot** | Detects specific RNA molecules and provides information about RNA size and abundance. |
| **qRT-PCR (Quantitative Reverse Transcription PCR)** | Measures the expression levels of selected genes with high sensitivity and accuracy. |
| **PCR-based Methods** | Amplify and detect RNA-derived complementary DNA (cDNA) for gene expression analysis and transcript identification. |                

### 5.2 High-throughput Methods

These measure many genes at once.

RNA Analysis Technologies

| Technology | Scale |
|------------|-------|
| **Microarray** | Measures the expression of thousands of genes simultaneously. |
| **RNA-seq** | Profiles the entire transcriptome, including known and novel transcripts. |
| **CAGE (Cap Analysis of Gene Expression)** | Identifies and quantifies transcription start sites (TSSs). |
| **10X Chromium** | Enables high-throughput single-cell RNA sequencing (scRNA-seq). |
| **Fluidigm** | Analyzes the expression of hundreds of genes, often at the single-cell level. |. 

---

## 6. Microarray Technology

Microarrays measure gene expression using probes fixed on a chip.

**Basic Workflow**

```
Extract RNA
↓
Convert RNA to cDNA
↓
Hybridize cDNA to microarray chip
↓
Scan fluorescent signal
↓
Measure gene expression
```


**Microarray Pre-processing**

```
Raw data
↓
Background correction
↓
Normalization
↓
Transformation
↓
Analysis
```

**Common R/Bioconductor packages:**

```
affy
oligo
lumi
limma
```

## 7. RNA-seq Technology

RNA-seq uses sequencing to measure RNA molecules.

**Basic Workflow**

```
Extract RNA
↓
Fragment RNA
↓
Convert RNA to cDNA
↓
Sequence reads
↓
Map reads to genome/transcriptome
↓
Count reads per gene
↓
Perform statistical analysis
```
RNA-seq can detect:

- Differential gene expression
- Isoform abundance
- Non-coding RNA
- RNA editing
- Alternative splicing
- SNPs in transcripts

## 8. RNA-seq Analysis Pipeline

```
Raw FASTQ files
↓
Quality control
↓
Read trimming
↓
Genome alignment
↓
Feature counting
↓
Normalization
↓
Differential expression analysis
↓
Visualization
↓
Pathway analysis
```
Common tools:

| Step                    | Tool                      |
| ----------------------- | ------------------------- |
| Quality control         | FastQC                    |
| Trimming                | Trim Galore / Cutadapt    |
| Alignment               | STAR / HISAT2             |
| Counting                | featureCounts / HTSeq     |
| Differential expression | DESeq2 / edgeR / limma    |
| Visualization           | ggplot2 / pheatmap        |
| Pathway analysis        | clusterProfiler / enrichR |

---

## 9. RNA-seq vs Microarray

| Feature                    | RNA-seq             | Microarray |
| -------------------------- | ------------------- | ---------- |
| Prior genome knowledge     | Not always required | Required   |
| Dynamic range              | High                | Lower      |
| Novel transcript detection | Yes                 | No         |
| Cost                       | Higher              | Lower      |
| Sensitivity                | High                | Moderate   |
| Data size                  | Large               | Smaller    |

RNA-seq is now widely used because it gives more detailed transcriptome information.

## 10. Differential Gene Expression Analysis

Differential expression analysis identifies genes that show different expression between conditions.

Example:

```
Control group vs Disease group
Normal tissue vs Cancer tissue
Treated cells vs Untreated cells
```
**Important values**

| Term               | Meaning                                       |
| ------------------ | --------------------------------------------- |
| log2 fold change   | Direction and size of expression change       |
| p-value            | Statistical significance                      |
| adjusted p-value   | Corrected significance after multiple testing |
| upregulated gene   | Higher expression in test condition           |
| downregulated gene | Lower expression in test condition            |

---

# 11. Example DESeq2 Workflow in R
```r
###########################################################
# Gene Expression Analysis using DESeq2
#
# Workflow:
# 1. Read featureCounts output
# 2. Differential expression analysis with DESeq2
# 3. Gene annotation using biomaRt
# 4. Volcano plot visualization
# 5. Heatmap of top differentially expressed genes
#
# Dataset:
# Breast Cancer (MCF7) vs Normal samples
###########################################################
# Load required packages
library(DESeq2)
library(ggplot2)

# Read featureCounts output file
# skip = 1 ignores the first summary line
counts <- read.table(
  "gene_counts.txt",
  header = TRUE,
  row.names = 1,
  skip = 1
)

# Remove annotation columns and keep only count columns
counts <- counts[, 6:ncol(counts)]

# Create sample metadata
# Two normal samples and two MCF7 cancer samples
coldata <- data.frame(
  condition = factor(c("normal", "normal", "MCF7", "MCF7")),
  row.names = colnames(counts)
)

# Create DESeq2 dataset object
dds <- DESeqDataSetFromMatrix(
  countData = round(counts),
  colData = coldata,
  design = ~ condition
)

# Run differential expression analysis
dds <- DESeq(dds)

# Compare MCF7 against normal samples
res <- results(
  dds,
  contrast = c("condition", "MCF7", "normal")
)

# Convert DESeq2 results to dataframe
res_df <- as.data.frame(res)

# Store Ensembl gene IDs as a column
res_df$Gene_id <- rownames(res_df)

# Remove version numbers from Ensembl IDs
# Example:
# ENSG000001234.5 -> ENSG000001234
res_df$Geneid_clean <- sub("\\..*", "", res_df$Gene_id)

# Install biomaRt if needed
# install.packages("biomaRt")

# Load biomaRt package
library(biomaRt)

# Connect to Ensembl human gene database
mart <- useMart(
  "ensembl",
  dataset = "hsapiens_gene_ensembl"
)

# Retrieve gene annotations
gene_info <- getBM(
  attributes = c(
    "ensembl_gene_id",
    "hgnc_symbol",
    "external_gene_name",
    "description"
  ),
  filters = "ensembl_gene_id",
  values = res_df$Geneid_clean,
  mart = mart
)

# Merge DESeq2 results with gene annotation
res_annotated <- merge(
  res_df,
  gene_info,
  by.x = "Geneid_clean",
  by.y = "ensembl_gene_id",
  all.x = TRUE
)

# Create labels for significant genes only
# padj < 0.05
# absolute log2FC > 1
res_annotated$label <- ifelse(
  res_annotated$padj < 0.05 &
    abs(res_annotated$log2FoldChange) > 1,
  res_annotated$hgnc_symbol,
  NA
)
# Install ggrepel if needed
# install.packages("ggrepel")

# Load ggrepel for non-overlapping labels
library(ggrepel)

# Generate volcano plot
ggplot(
  res_annotated,
  aes(
    x = log2FoldChange,
    y = -log10(pvalue)
  )
) +
  geom_point(alpha = 0.5) +
  geom_text_repel(
    aes(label = label),
    size = 3,
    na.rm = TRUE
  ) +
  theme_minimal() +
  xlab("Log2 Fold Change") +
  ylab("-Log10 P-value") +
  ggtitle("Volcano Plot with Gene Names")


```


## 12. Volcano Plot

A volcano plot shows both expression change and statistical significance.

```
X-axis = log2 fold change
Y-axis = -log10 p-value
```

<img width="1546" height="801" alt="image" src="https://github.com/user-attachments/assets/361fcbb3-90e8-4476-aa3e-3df04d1a8f87" />


Genes on the far right are strongly upregulated.

Genes on the far left are strongly downregulated.

Genes at the top are statistically significant.

---


## 13. Heatmap and Clustering

Heatmaps help visualize expression patterns across genes and samples.

Genes with similar expression patterns cluster together.


```r
# Load heatmap package
library(pheatmap)

# Sort genes by adjusted p-value
res_sorted <- res_annotated[
  order(res_annotated$padj),
]

# Select top 50 most significant genes
top_genes <- res_sorted$Gene_id[1:50]

# Corresponding gene symbols
top_names <- res_sorted$hgnc_symbol[1:50]

# Variance stabilizing transformation
# Improves visualization and clustering
vsd <- vst(dds)

# Extract expression matrix for top genes
heatmap_matrix <- assay(vsd)[top_genes, ]

# Replace Ensembl IDs with gene symbols
rownames(heatmap_matrix) <- top_names

# Draw heatmap
pheatmap(
  heatmap_matrix,
  scale = "row",
  clustering_distance_rows = "euclidean",
  clustering_distance_cols = "euclidean",
  main = "Top Differentially Expressed Genes"
)
```

<img width="1530" height="995" alt="image" src="https://github.com/user-attachments/assets/397f0ed7-e0a7-4325-ab2c-8b9ca8184152" />


**Heatmap Interpretation: Top Differentially Expressed Genes**

This heatmap shows the 50 most significantly differentially expressed genes identified by your DESeq2 analysis between Normal breast cells and MCF7 breast cancer cells.

**Figure: Heatmap of the top 50 differentially expressed genes identified by DESeq2 analysis. Rows represent genes and columns represent samples. Red indicates relatively high expression and blue indicates relatively low expression after variance stabilizing transformation and row scaling. Hierarchical clustering clearly separates normal breast samples from MCF7 breast cancer samples, demonstrating distinct transcriptional profiles between the two conditions.**

---

## 14. Clustering in Gene Expression Analysis

Clustering is used to group genes or samples based on similar expression profiles.

| Method                  | Description                                    |
| ----------------------- | ---------------------------------------------- |
| Hierarchical clustering | Builds a tree-like dendrogram                  |
| K-means clustering      | Groups genes into a fixed number of clusters   |
| PCA                     | Reduces dimensions and shows sample separation |

---

## 15. Pathway and Ontology Analysis

After finding differentially expressed genes, we need to understand what they do.

**Pathway analysis helps answer:**

```
Which biological processes are affected?
Which pathways are enriched?
Are immune, cancer, metabolic, or inflammatory pathways involved?
```

**Common databases:**

| Database      | Purpose                                                    |
| ------------- | ---------------------------------------------------------- |
| KEGG          | Biological pathways                                        |
| Reactome      | Curated pathways                                           |
| Gene Ontology | Biological process, molecular function, cellular component |
| MSigDB        | Gene set collections                                       |

---

## 16. Fisher’s Exact Test for Enrichment

Fisher’s Exact Test checks whether a gene list is enriched for a pathway.

Example question:

```
Are differentially expressed genes enriched in the NF-kB pathway?
```
**R Example**

```r
# Example contingency table
tab <- matrix(c(70, 30, 80, 40), nrow = 2)

# Fisher's Exact Test
fish_res <- fisher.test(tab, alternative = "greater")

# Show p-value
fish_res$p.value
```

---

## 17. Gene Ontology Categories

Gene Ontology has three main categories:

| GO Category        | Meaning                                         |
| ------------------ | ----------------------------------------------- |
| Biological Process | What biological process the gene is involved in |
| Molecular Function | What molecular activity the gene performs       |
| Cellular Component | Where the gene product is located               |


Example:

```
Biological Process: immune response
Molecular Function: DNA binding
Cellular Component: nucleus
```
---

## 18. Single-cell RNA-seq

Single-cell RNA-seq measures gene expression in individual cells.

Traditional RNA-seq measures the average expression from many cells.

Single-cell RNA-seq shows cell-to-cell differences.

Why it matters

```
Bulk RNA-seq = average expression
Single-cell RNA-seq = expression in each individual cell
```
This is useful because tissues contain mixed cell populations.

Example:

```
Tumour tissue may contain:
- Cancer cells
- Immune cells
- Fibroblasts
- Endothelial cells
```
Single-cell RNA-seq can separate these cell types.

---

## 19. Important Visual Outputs

| Output           | Purpose                                  |
| ---------------- | ---------------------------------------- |
| PCA plot         | Shows sample separation                  |
| Volcano plot     | Shows significant up/downregulated genes |
| Heatmap          | Shows gene expression patterns           |
| MA plot          | Shows fold change vs expression level    |
| Pathway bar plot | Shows enriched biological pathways       |

---

## 20. Conclusion

Gene expression analysis helps us understand how genes behave under different biological conditions.

RNA-seq and microarrays are major technologies for measuring transcriptome-wide expression. RNA-seq is now more widely used because it provides high-resolution information about transcripts, isoforms, non-coding RNAs, and expression levels.

The main analysis steps include quality control, alignment, counting, normalization, differential expression analysis, visualization, clustering, and pathway enrichment.

This repository provides a structured guide for learning and applying gene expression analysis in bioinformatics.
