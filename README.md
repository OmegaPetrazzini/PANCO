# PANCO

PANCO allows PAthogenicity prediction of Non-COding variants using a combination of functional and evolutionary features fitted on a Gradient Boosted Trees model.

Pre-computed PANCO predictions for all possible non-coding variants in dbNSFP are available at https://doi.org/10.5281/zenodo.5745849.


To compute your own PANCO predictions please follow these instructions:

1) Annotated all features using ANNOVAR [1], please see https://annovar.openbioinformatics.org/en/latest/.

2) Remove variants high >66% missing values and impute the remaining using NAsImpute [2].

3) Download PANCO (PANCO.RDS) from https://doi.org/10.5281/zenodo.5745849.

4) Import your imputed dataset and PANCO into an R session.

```
library(data.table)
library(caret)

fit_model = readRDS("/path/PANCO.RDS")
MYDATA = fread("/path/MYDATA.txt", data.table = FALSE)
```

5) Make sure feature names match.
```
colnames(fit_model$trainingData)[which(!colnames(fit_model$trainingData) %in% colnames(I))]
```

6) No scaling is requiered so just predict.
```
Y = predict(fit_model, MYDATA, type = "prob")
```

Details on how PANCO was built will be made available at publication - 
Ben Omega Petrazzini, Fernando López-Bello, Hugo Naya, & Lucia Spangenberg. (2021). _Prediction of pathogenic variants in non-coding regions of the human genome. (under revison)._


References:
[1] Wang, K., Li, M. & Hakonarson, H. ANNOVAR: functional annotation of genetic variants from high-throughput sequencing data. Nucleic Acids Research 38, e164-e164 (2010).
[2] Petrazzini, B.O., Naya, H., Lopez-Bello, F. et al. Evaluation of different approaches for missing data imputation on features associated to genomic data. BioData Mining 14, 44 (2021). https://doi.org/10.1186/s13040-021-00274-7
