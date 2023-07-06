# Chiller Efficiency Drift Detection
# 1. Installations
- Install all packages mentionned in the requirements.txt file
- For installing affiliation metrics package, follow the instructions below:
    - download package from: https://github.com/ahstat/affiliation-metrics-py
    - go to affiliation directory (**cd**)
    - execute command:
      
            > pip install .
    - relaunch notebook kernel if necessary
 
# 2. Data Directory
- Note: Data directory should be placed at the same level as folder containing all notebooks (NOT at the same level as notebooks!)
**- efficiency_error_dataset/:** dataset containing calculated efficiency, predicted efficiency and efficiency prediction error
  
      - test_3_months.csv: model efficiency prediction on last 3 months of dataset
      - test_2022.csv: model efficiency prediction on year 2022 of dataset
  
**- preprocessed_dataset/:** dataset after preprocessing (numeric transformations, outlier removal, efficiency calculation, temperature integration)

      - preprocessed_dataset.csv: preprocessed dataset 1
      - preprocessed_dataset2.csv: preprocessed dataset 2

**- temp_component_model/:** contains 1 csv file per building
  
      - BUILDING_ID.csv: temperature component model for building
  
**- telecom_paris_dataset.xlsx:** provided dataset 1

**- telecom_paris_dataset_v2.xlsx:** provided dataset 2

# 3. Notebooks

### NOTEBOOK: construct_temp_component_models
**1. Category:** data transformation

**2. Method:** deseasonalisation

**3. Steps in Notebook:**
- construct component models from temperature data

**4. Goals/ Observations/ Insights:**
- write temperature component model to output file

**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:**
- data/temp_component_model/BUILDING_ID.csv

### NOTEBOOK: correlations
**1. Category:** data transformation

**2. Method:** deseasonalisation

**3. Steps in Notebook:**
- visualisation: deseasonalised energy input
- visualisation: deseasonalised energy output
- visualisation: deseasonalised temperature
- visualisation: deseasonalised efficiency
- visualisation: efficiency, temperature, percentage load
- visualisation: ds efficiency, ds temperature, percentage load
- visualisation: ds efficiency vs ds temperature
- visualisation: efficiency vs percentage load
- visualisation: ds efficiency vs ds percentage load

**4. Goals/ Observations/ Insights:**
- efficiency has greater variance after deseasonalisation
  
**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:** NONE

### NOTEBOOK: data_visualisation
**1. Category:** data exploration

**2. Method:** None

**3. Steps in Notebook:**
- visualisation: data distributions
- visualisation: energy input and energy output
- visualisation: normalized energy input and normalized energy output
- visualisation: standardized energy input and standardized energy output
- visualisation: efficiency
- visualisation: log(efficiency/ energy input)
- visualisation: temperature
- visualisation: percentage load (pourcentage charge)
- visualisation: input energy and percentage load
- visualisation: input energy by percentage load
- visualisation: output energy by percentage load
- visualisation: efficiency by percentage load

**4. Goals/ Observations/ Insights:**
- compare normalisation vs standardisation
  
**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:** NONE

### NOTEBOOK: deseasonalised_energy
**1. Category:** data transformation

**2. Method:** deseasonalisation

**3. Steps in Notebook:**
- visualisation: deseasonalised energy distribution
- unormalisation after deseasonalisation
- translation after deseasonalisation
- visualisation: translated energy output after deseasonalisation
- visualisation: normalized energy input, normalized energy output and temperature component
- visualisation: distribution of efficiency calculated from translated energy after deseasonalisation
- visualisation: ds efficiency, translated ds efficiency, efficieny
- visualisation: distribution of deseasonalised efficiency per month
- visualisation: distribution of translated deseasonalised efficiency per month
- visualisation: distribution of efficiency per month
- visualisation: deseasonalised efficiency and percentage load
- visualisation: deseasonalised efficiency at 20%-40% load
- visualisation: translated deseasonalised efficiency vs translated deseasonalised percentage load per month
- visualisation: deseasonalised efficiency vs deseasonalised percentage load per month
- visualisation: efficiency vs percentage load per month

**4. Goals/ Observations/ Insights:**
- the goal of this notebook is to explore how we can transform the data after deseasonalisation to get coherent values of efficiency (range [0,15])
- deseasonalisation gives negative efficiency values
- applying translations to get a coherent range of efficiency values does not give coherent results

**5. Input Files:**
- data/telecom_paris_dataset.xlsx
- data/temp_component_model/BUILDING_ID.csv

**6. Output Files:** NONE

### NOTEBOOK: drift_detection_and_evaluation
**1. Category:** data generation/ drift detection/ drift prediction evaluation

**2. Method:** kdq trees

**3. Steps in Notebook:**
- visualisation: data to simulate (efficiency prediction error)
- visualisation: generated data
- visualisation: generated data with drift
- visualisation: drift detection on efficiency error (kdq trees)
- evaluation score of drift detection

**4. Goals/ Observations/ Insights:**
- simulate data statistically similar to efficiency prediction error
- insert a known drift in the generated data
- run drift detection algorithm on generated data
- evaluate drift detection on generated data
- run drift detection algorithm on real data

**5. Input Files:**
- data/efficiency_error_dataset/test_3_months.csv

**6. Output Files:** NONE

### NOTEBOOK: drift_detection_kdq_tree
**1. Category:** drift detection

**2. Method:** kdq trees

**3. Steps in Notebook:**
- visualisation: drift detection on efficiency and ds efficiency
- visualisation: drift detection on efficiency and ds efficiency at 40%-60% load
- visualisation: drift detection on efficiency and ds efficiency at 20%-40% load

**4. Goals/ Observations/ Insights:**
- drift detection on efficiency
- drift detection on deseasonalised efficiency
- the results are identical whether we run the kdq tree algorithms on efficiency or deseasonalised efficiency!

**5. Input Files:**
- data/telecom_paris_dataset.xlsx
- data/temp_component_model/BUILDING_ID.csv

**6. Output Files:** NONE

### NOTEBOOK: eff_prediction_model
**1. Category:** data transformation

**2. Method:** efficiency prediction

**3. Steps in Notebook:**
- train xgboost model on 01/2021-05/2022 data and test on 06/2022-09/2022
- model r2 score: 0.957
- visualisation: efficiency prediction error (all equipments)
- visualisation: predicted efficiency and true efficiency (single equipment)
- visualisation: efficiency prediction error (single equipment)
- visualisation: drift detection on efficiency prediction error

**4. Goals/ Observations/ Insights:**
- write preprocessed data to output file (dataset1)
- write efficiency prediction error to file (dataset1)

**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:**
- data/preprocessed_dataset/preprocessed_dataset.csv
- data/efficiency_error_dataset/test_3_months.csv

### NOTEBOOK: eff_prediction_model_annual
**1. Category:** data transformation

**2. Method:** efficiency prediction

**3. Steps in Notebook:**
- train xgboost model on 01/2021-12/2021 data and test on 01/2022-12/2022
- model r2 score: 0.938
- visualisation: efficiency prediction error (all equipments)
- visualisation: predicted efficiency and true efficiency (single equipment)
- visualisation: efficiency prediction error (single equipment)
- visualisation: drift detection on efficiency prediction error

**4. Goals/ Observations/ Insights:**
- write preprocessed data to output file (dataset2)
- write efficiency prediction error to file (dataset1)

**5. Input Files:**
- data/telecom_paris_dataset_v2.xlsx

**6. Output Files:**
- data/preprocessed_dataset/preprocessed_dataset2.csv
- data/efficiency_error_dataset/test_2022.csv

### NOTEBOOK: energy_temperature_relation
**1. Category:** data exploration

**2. Method:** NONE

**3. Steps in Notebook:**
- visualisation: Energy In, Out, log(temperature)
- visualisation: efficiency vs temperature by percentage load
- visualisation: standardized energy in, out, temperature
- visualisation: normalized energy in, out, temperature
- visualisation: Correlation: energy in, out, efficiency, temperature
- visualisation: normalized efficiency and temperature
- visualisation: Spring Correlation: energy in, out, efficiency, temperature
- visualisation: Summer Correlation: energy in, out, efficiency, temperature

**4. Goals/ Observations/ Insights:**
- compare normalisation vs standardisation
- normalisation better suited than standardisation

**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:** NONE

### NOTEBOOK: kernel_pca_drift_visualisation
**1. Category:** data transformation

**2. Method:** kernel pca

**3. Steps in Notebook:**
- apply kernel PCA to data
- compare PCA component correlations to deduce if the components relates to temperature and percentage load
- compare PCA component timeseries shape to deduce if the components relates to temperature and percentage load

**4. Goals/ Observations/ Insights:**
- attempt to remove effect of temperature from efficiency data
- kernel pca used for non-linear relationship
- we have no guarantee on the interpretation of the PCA components

**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:** NONE

### NOTEBOOK: pca_drift_visualisation
**1. Category:** data transformation

**2. Method:** pca

**3. Steps in Notebook:**
- apply PCA to data
- compare PCA component correlations to deduce if the components relates to temperature and percentage load
- compare PCA component timeseries shape to deduce if the components relates to temperature and percentage load

**4. Goals/ Observations/ Insights:**
- attempt to remove effect of temperature from efficiency data
- hypothesis: linear relationship
- we have no guarantee on the interpretation of the PCA components

**5. Input Files:**
- data/telecom_paris_dataset.xlsx

**6. Output Files:** NONE


