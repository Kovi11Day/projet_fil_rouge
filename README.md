# Chiller Efficiency Drift Detection
# 1. Installations
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
