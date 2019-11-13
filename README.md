# HackathonNov2019
Data for Hackathon on November 21, 2019

In this repository are some data from several populations in the 1000 Genomes Project, and a simulated trait phenotype.  The files are in PLINK format. The primary genotype file is too large for github, and can be found here: https://www.dropbox.com/s/1vaa9q6nv5lnphw/samplePop.bed?dl=0 

The general goal of this project is to look at how polygenic risk scores (PRS) developed in one population perform when applied to another population, and then to brainstorm on why there are differences in performance and possibly how to improve performance.

The files provided are:
  SamplePop.bim    Marker names and locations
  SamplePop.fam    ID numbers (family ID and individual ID, identical in this case)
  sampleCovar.txt  Some covariates like age and sex
  samplePheno.txt  The primary simulated trait phenotype
  Population.txt   A file with just ID numbers and population identifiers
  
One of the easiest ways to get started is with PLINK, which can be downloaded from https://www.cog-genomics.org/plink/1.9/.
A simple GWAS in PLINK can be run as follows from the command line:

plink --allow-no-sex --bfile samplePop --covar sampleCovar.txt  --linear --out testGWAS --pheno samplePheno.txt

This command ignores anyone missing sex information, tells plink that the genotype input files are called "samplePop" (there are 3 files, samplePop.bed, samplePop.bim, samplePop.fam) and are in a specific format, requests a linear model for the genotypes, tells the software that the phenotype is in samplePheno.txt, and that output should be written to files called "testGWAS.log".  To be more specific, I run this on my computer at the command line as:

cd c:\users\celia.greenwood\Dropbox\HackathonNov2019MNI
c:\CeliaFiles\Programs\PLINK\plink --allow-no-sex --bfile samplePop --covar sampleCovar.txt  --linear --out testGWAS --pheno samplePheno.txt
        (You will need to alter pathnames for your own computer).

The 1000 Genomes contains individuals from several populations:
ACB ASW CEU CHB ESN FIN GBR GWD IBS JPT MSL TSI YRI 
 96  61  99 103  99  99  91 113 107 104  85 107 108 
 
CHB and JPT are from ASIA.  CEU, FIN, GBR, IBS, TSI are from Europe.  The remainder are from Africa. You can visualize population differences by scatter plots of the top principal components using several thousand genotypes, and you can find the acronym definitions here:  https://www.internationalgenome.org/category/population/

To analyze only a subset of the populations, this can be done within plink using the "within" and the "cluster" commands, e.g. to analyze only GBR and TSI, I can write:
c:\CeliaFiles\Programs\PLINK\plink --allow-no-sex --bfile samplePop --linear --out testGWAS2 --pheno samplePheno.txt --within Population.txt --keep-cluster-names GBR TSI

