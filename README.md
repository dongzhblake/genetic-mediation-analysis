# genetic-mediation-analysis
This is the implementation page of REML-mediation tool to remove genetic coufounidng effect in corss-trait epidemeological studies.

Three are three main functions in the R script genetic_mediation_function. The first function conducts mediation analysis on single variant. The second function conducts mediation analysis across the gemone by taking the GWAS result file. The third function can read the log file of BOLT-REML and output the estimated causal effect and its standard error. 

Load and use these functions by 
````
library("devtools")
devtools::source_url("https://github.com/dongzhblake/genetic-mediation-analysis/blob/main/genetic_mediation_function.R?raw=TRUE")
````
User manual of BOLE-REML can be found at 
````
https://alkesgroup.broadinstitute.org/BOLT-LMM/BOLT-LMM_manual.html
````
Using our example data, we can run BOLT-REML to estimate variance component
````
./bolt --bfile=example/test --phenoFile=example_folder/test_pheno --phenoCol=M --phenoCol=Y --covarFile=example_folder/test_pheno --qCovarCol=U --reml --noMapCheck 2>&1 | tee output.log
````
We can extract the causal effect estimate from BOTL-REML output using the third R function. Note that any variance-component analysis tool result can be used, such as GCTA. 
````
BOLT=read_BOLT("example_folder/output.log")
````
Summary statistics of the mediator sumstats_M_test and for the outcome sumstats_Y_test were obtained using plink2 and processed to add headers plus some unnecessary columns removed. 
````
GWAS_M=read.table("example_folder/sumstats_M_test",header=T)
GWAS_Y=read.table("example_folder/sumstats_Y_test",header=T)
````
To run single-varient level mediation analysis, for example, on the first variant. Users can input causal effect estimate obtained from any method, such as linear regression.
````
SNP_mediation(GWAS_M$BETA[1],GWAS_M$SE[1],BOLT$alpha.h,BOLT$SE_ah)
````
For genome-level genetic mediation analysis, 
````
GWAS_mediation(GWAS_M,BOLT$alpha.h,BOLT$SE_ah,GWAS_Y)
````

Please contact zihan.dong@yale.edu if there are any problems.
