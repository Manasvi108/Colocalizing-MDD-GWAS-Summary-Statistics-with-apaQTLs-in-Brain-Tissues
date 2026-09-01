# Colocalizing-MDD-GWAS-Summary-Statistics-with-apaQTLs-in-Brain-Tissues

### MOTIVATION

**Major Depressive Disorder** (MDD) exhibits striking sex differences in both prevalence and phenotypic expression, with females experiencing roughly twice the rate of diagnosis compared to males. A critical driver of these biological disparities lies in the sex-differentiated genetic architecture of complex traits. These genetic influences manifest through both sex-specific effects (variants operating exclusively in one sex) and sex-dependent effects (variants influencing both sexes, but with differing effect magnitudes or directions). 
While standard **Genome-Wide Association Studies** (GWAS) identify genetic risk variants across combined populations, sex-stratified GWAS analyzes males and females separately, providing crucial insights into sex-differentiated regulatory mechanisms underlying disease risk. 
Beyond direct genetic associations, post-transcriptional mechanisms, such as **Alternative Polyadenylation** (APA) play a fundamental role in regulating gene expression. APA generates RNA transcripts with distinct 3' ends from a single gene, impacting mRNA stability, translation, and cellular localization. APA exhibits high tissue specificity and is essential for neurodevelopment and brain function. Specific genetic variants that modulate these polyadenylation processes are known as **alternative polyadenylation Quantitative Trait Loci** (apaQTLs). Despite their regulatory importance, the role of brain-derived apaQTLs in mediating MDD risk across sexes remains poorly defined.
To integrate disease risk with regulatory genomics, colocalization analysis provides a statistical framework to determine whether two distinct signals such as an MDD risk locus from a GWAS and an apaQTL locus share the exact same causal genetic variant in a shared genomic region, rather than distinct variants in linkage disequilibrium. By colocalizing brain tissue apaQTLs with both sex-stratified and sex-combined MDD GWAS summary statistics, this study aims to systematically uncover sex-shared and sex-differentiated post-transcriptional regulatory mechanisms driving MDD. 

### METHODOLOGY

### Data
The apaQTL data was obtained from **GTEx version 11** for 6 tissues : Amygdala, Cortex, Frontal Cortex BA9, Hippocampus, Hypothalamus and Substantia Nigra.
The **sex-stratified GWAS Summary Statistics** were obtained from the paper - Thomas, J.T., Thorp, J.G., Huider, F. et al. Sex-stratified genome-wide association meta-analysis of major depressive disorder. Nat Commun 16, 7960 (2025). https://doi.org/10.1038/s41467-025-63236-1
The **sex-combined GWAS Summary Statistics** were obtained from the paper - Mark J Adams, Fabian Streit, Xiangrui Meng, et al. Trans-ancestry genome-wide study of depression identifies 697 associations implicating cell types and pharmacotherapies. Cell, 2025 Feb 6;188(3):640-652.e9. https://doi.org/10.1016/j.cell.2024.12.002

### Genomic Coordinate Harmonization 
Because the MDD GWAS summary statistics (both sex-combined and sex-stratified) were mapped to GRCh37/hg19 and the apaQTL data were mapped to GRCh38/hg38, GWAS variant coordinates were lifted over to hg38 to ensure genomic alignment across datasets. For each fine-mapped GWAS lead SNP, a 2Mb genomic window (±1Mb) was constructed to extract overlapping GWAS variants and apaQTLs for downstream analysis. 

### Constructing Linkage Disequilibrium (LD) Matrices 
Linkage disequilibrium (LD) matrices were generated for each 2Mb window using PLINK v2.0. In the absence of individual-level genotypes of the GWAS cohort data due to patient privacy laws, the 1000 Genomes Project (1KGP) European superpopulation panel was used as an ancestry-matched reference proxy. LD computation was restricted exclusively to variants present in both the GWAS and apaQTL datasets, dropping all non-overlapping variants.

### SuSiE Colocalization Analysis 
Colocalization was evaluated within each 2 Mb window to determine whether MDD risk and alternative polyadenylation (APA) events share a common causal variant. Using the Sum of Single Effects (SuSiE) colocalization framework, posterior probabilities were calculated for all overlapping variants associated with each candidate APA phenotype. Evidence of colocalization was evaluated based on the posterior probability of Hypothesis 4 (PPH4), which indicates a shared causal variant driving both MDD risk and APA regulation.
