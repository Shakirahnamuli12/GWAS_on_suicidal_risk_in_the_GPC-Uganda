# GENETIC RISK FACTORS OF SUICIDAL RISK AMONG THE GENERAL POPULATION COHORT FROM SOUTHWESTERN UGANDA

Contributors: Shakirah Namuli¹, Irene Namara¹², Lillian Linda¹, Herbert Agasi¹, Richard Mayanja¹², Christopher Kintu¹², Eugene Kinyanda², Segun Fatumo¹²³, Tinashe Chikowore¹⁴, Allan Kalungi¹²⁵
Affiliations: ¹ The African Computational Genomics (TACG) Research Group,² MRC/UVRI & LSHTM Uganda Research Unit, ³ Precision Healthcare University Research Institute, Queen Mary University of London, ⁴ Harvard Medical School, ⁵ Department of Medical Biochemistry, Makerere University

We carried out a genome wide association study to identify geneti risk factors associated with suicidal risk with the general population cohort of SouthWestern Uganda using the FASTGWA-GLMM Workflow

# FASTGWA-GLMM Workflow
fastGWA-GLMM is a tool designed for ultra-fast generalized linear mixed model-based association analysis, specifically for binary traits.
It uses a sparse Genetic Relationship Matrix (GRM) to conduct Genome-Wide Association Studies (GWAS) efficiently, accounting for population stratification. 
This approach is particularly useful in large-scale biobank studies.
NOTE : Before you run you GWAS script, you need to generate a Sparse GRM as shown below.


## Step 1: Obtain PLINK Files
You need to generate .bim, .bed, and .fam files from your genotype data.

Code: ./plink --bfile UGR --keep output_suicide_ugrfam --make-bed --out GPC_result.suicide --noweb4

UGR: The prefix of your original PLINK files.
output_suicide_ugrfam: The .fam file for your study.
GPC_result.suicide: The output prefix for the new PLINK files.

## Step 2: Create a GRM
Next, generate the Genetic Relationship Matrix (GRM) using GCTA from the plink file.

Code: ./gcta64 --bfile GPC_result.suicide --make-grm 0.05 --out suicide_data_grm

###This creates the GRM using a cutoff of 0.05.

## Step 3: Generate a Sparse GRM
Create a sparse GRM, which is optimized for large-scale genetic analyses.
Code: ./gcta64 --grm suicide_data_grm --make-bK-sparse 0.05 --out GPC_sp_grm

suicide_data_grm: The input GRM.
GPC_sp_grm: The output prefix for the sparse GRM.

## Step 4: Submit the Job Script
You can submit the job script to your computing cluster to run the fastGWA-GLMM analysis.


