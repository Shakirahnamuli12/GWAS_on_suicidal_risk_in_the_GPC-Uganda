# GWAS USING A GLMM

# FASTGWA-GLMM Workflow
fastGWA-GLMM is a tool designed for ultra-fast generalized linear mixed model-based association analysis, specifically for binary traits.
It uses a sparse Genetic Relationship Matrix (GRM) to conduct Genome-Wide Association Studies (GWAS) efficiently, accounting for population stratification. 
This approach is particularly useful in large-scale biobank studies.
NOTE : Before you run you GWAS script, you need to generate a Sparse GRM as shown below.


## 1: Obtain PLINK Files
You need to generate .bim, .bed, and .fam files from your genotype data.

Code: ./plink --bfile UGR --keep output_original_darfam --make-bed --out pop_result.data --noweb4

UGR: The prefix of your original PLINK files.
output_original_darfam: The .fam file for the study.
pop_result.data: The output prefix for the new PLINK files.

## 2: Create a GRM
Next, generate the Genetic Relationship Matrix (GRM) using GCTA from the plink file.

Code: ./gcta64 --bfile pop_result.data --make-grm 0.05 --out pop_data_grm

###This creates the GRM using a cutoff of 0.05.

## 3: Generate a Sparse GRM
Create a sparse GRM, which is optimized for large-scale genetic analyses.
Code: ./gcta64 --grm pop_data_grm --make-bK-sparse 0.05 --out pop_sp_grm

suicide_data_grm: The input GRM.
pop_sp_grm: The output prefix for the sparse GRM.

## 4: Submit the Job Script
You can submit the job script to your computing cluster to run the fastGWA-GLMM analysis.


