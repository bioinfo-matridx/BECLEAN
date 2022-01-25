# Reproducible Analyses of BECLEAN Manuscript

This repository hosts the reproducible workflow of BECLEAN manuscript. Input data and iPython notebook are in the BECLEAN/ directory. You can reproduce the analyses by running the code in the notebook. The html-format notebook document can also be viewed in web browser here: [Reproducible Analyses of BECLEAN Manuscript](https://bioinfo-matridx.github.io/BECLEAN/BECLEAN/BECLEAN_analysis.html) and [Analyses using decontam](https://bioinfo-matridx.github.io/BECLEAN/BECLEAN/decontam_analysis.html).

### Background Species Modeling

#### Description

Get a linear model of background contaminant species using contaminant reads and sample input mass.

#### Usage

```python
get_model_of_taxid(df, taxid, key='log_library_concentration')
```

#### Input

- df: pandas dataframe containing sample meta data and rpm of given species, columns are: sample_name, rpm (RPM of given species in specified sample), library_concentration (pM), nucleic_acid_mass (ng), log_rpm (log<sub>2</sub>-transformed rpm), log_library_concentration (log<sub>2</sub>-transformed library concentration), log_nucleic_acid_mass (log<sub>2</sub>-transformed nucleic acid mass)

```python
df.head()
                 sample_name     rpm  library_concentration  \
0  0p1ng-labA-automated_rep1   55.98                 4.5200   
1  0p1ng-labA-automated_rep2  215.76                 4.9946   
2  0p1ng-labA-automated_rep3   88.92                 6.3054   
3  0p1ng-labA-automated_rep4  116.87                 7.1868   
4  0p1ng-labA-automated_rep5   63.99                 8.7100   

   nucleic_acid_mass   log_rpm  log_library_concentration  \
0                0.1  5.806840                   2.176323   
1                0.1  7.753284                   2.320369   
2                0.1  6.474436                   2.656588   
3                0.1  6.868761                   2.845350   
4                0.1  5.999775                   3.122673   

   log_nucleic_acid_mass  
0              -3.321928  
1              -3.321928  
2              -3.321928  
3              -3.321928  
4              -3.321928
```

- taxid: taxid of species
- key: column name of the value represents the sample input, choices are: 'log_library_concentration'(default), 'log_nucleic_acid_mass'

#### Output

Dictionary including taxid, model parameters, and data summary. Keys are: taxid, slope, intercept, sd, rvalue, pvalue, con_mean (average of value specified as sample input), rpm_mean (average of model normalized rpm), cutoff (maximum value of sample input within the linearity range), frequence (occurrence of frequency), and normaltest_p (normality test p value)

```python
print(model)
{'taxid': '4952', 'slope': -1.8593578255020993, 'intercept': 10.69367714681812, 'sd': 1.3304118739337008, 'rvalue': -0.920862481357378, 'pvalue': 1.653031532375798e-22, 'con_mean': 5.213102546583302, 'rpm_mean': 1.1744520907578715, 'cutoff': 7.928741122167166, 'frequence': 57, 'normaltest_p': 0.9721470013252992}
```

