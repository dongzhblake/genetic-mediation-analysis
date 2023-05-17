# genetic-mediation-analysis
This is the implementation page of REML-mediation tool to remove genetic coufounidng effect in corss-trait epidemeological studies.

Three are three main functions in the R script genetic_mediation_function. The first function conducts mediation analysis on single variant. The second function conducts mediation analysis across the gemone by taking the GWAS result file. The third function can read the log file of BOLT-REML and output the estimated causal effect and its standard error. 

Load and use these functions by 
````
devtools::source_url("https://github.com/dongzhblake/genetic-mediation-analysis/blob/main/genetic_mediation_function.R?raw=TRUE")
````
User manual BOLE-REML can be found at 
````
https://alkesgroup.broadinstitute.org/BOLT-LMM/BOLT-LMM_manual.html
````
Using our example data, we can run BOLT-REML to estimate variance component
````
./bolt --bfile=example/test --phenoFile=example/test_pheno --phenoCol=M --phenoCol=Y --covarFile=example/test_pheno --qCovarCol=U --reml --noMapCheck 2>&1 | tee output.log

````

