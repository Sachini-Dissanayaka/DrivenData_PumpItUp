# DrivenData/Pump-It-Up
#
**Introduction**

This project is based on the competition Driven Data® had published about water pumps, in Tanzania, a large country that suffers from access to good quality water. The main project idea is to identify which pumps are functional, which need some repairs, and which don't work at all. 
The metric used for this competition is “Accuracy” for calculating the precision of the model.

The result of the project was uploaded in order to score the predictions, which generated a response that is within 4% of the global participant results in this competition. The result was great because it had been **0.8234**, comparing with the first place 0.8294. It is a very good result considering the difference between these results.

**Dataset description**

The data for the training has 59,400 rows and 40 columns without the label that comes in a separate file, in the case of testing data it has 14,850 rows. The name of the target is status_group that has three possible values functional, non-functional, and functional but it needs to repair.

**Exploratory Data Analysis (EDA)**

You can find the fully generated profile report in the _profiling.ipynb_ file which was generated using the pandas_profiling library.

you can find the **best scored (0.8234)** model in the _ML_PumpItUp_BestScore.ipynb_ file. But it is not containg the techniques that had been used for analysis.

All EDA techniques that can be categorized as data collection, data cleaning, data preprocessing, and data visualization are available in the **_ML_PumpItUp_Initial.ipynb_** file. And also you can find different encoding techniques,normalization techniques, feature imprtance, Principle Component Analysis(PCA) techniques, SHAP and Partial Dependency Plots (PDP) in this file.

Here onwards I will explain some techniques that had been used in the _ML_PumpItUp_Initial.ipynb_ file which had been 0.8222

The target variable has three possible outcomes:
* Functional
* Non-functional
* Functional but it needs to repair

The feature amount_tsh is highly skewed (γ1 = 57.808) and has 41639 / 70.1% zeros that are why the log had been used to smooth it.

The year, month, and date were extracted from the feature date_recorded, and then the date_recorde had been dropped. 

The features gps_height, longitude, latitude,region_code, and district_code had been kept as it is.

The feature num_private  is highly skewed (γ1 = 91.934) and has 58643 which means 98.7% zeros. So the feature num_private had been dropped.

The feature scheme_name has 47.4% missing values and has a high cardinality (2697 distinct values). So the feature scheme_name also had been dropped. 

Since the feature recorded_by has a constant value GeoData Consultants Ltd, it had been also dropped.

The feature wpt_name has a high cardinality which means 37400 distinct values. So the feature wpt_name had been also dropped.

Since the feature construction_year has 34.9% zeros and the feature population has 36% zeros, the zeros in both the features construction_year and population were filled with NaNs.

The missing values in the features funder, installer, subvillage, public_meeting, scheme_management, permit, and construction_year had been filled with their most frequent values. And the missing values in the feature population are filled with its mean.

**Following are the creation of new features by mathematical transformation**

Extraction_all = extraction_type+ extraction_type_group + extraction_type_class

Management_all = management + management_group

Payment_all = payment + payment_type

Quality_all = water_quality + quality_group

Quantity_all = quantity + quantity_group

Source_all = source+ source_type

Waterpoint_all = waterpoint_type+ waterpoint_type_group

Then the features extraction_type, extraction_type_group, extraction_type_class, management, management_group, payment, payment_type, water_quality, quality_group, quantity, quantity_group, source, source_type, waterpoint_type, and waterpoint_type_group had been dropped.

**Normalization**

* The feature population had been normalized using mean normalization
* The feature amt had been normalized using min max normalization

**Encoding**

* The features basin, scheme_management, Management_all, Payment_all, Quality_all, Quantity_all, Source_all, Waterpoint_all had been encoded usin One-Hot Encode technique

* The features public_meeting and permit had been encoded using the Ordinal Encoding technique

* The feature source_class is encoded using target encoding

* The features funder, installer, subvillage, region, lga, ward, and Extraction_all had been encoded using the Binary Encoding technique


Labels had been encoded using the Label Encoding technique for Principle Component Analysis (PCA) which is a feature extraction technique.

You can find a feature importance graph that can be used as a post-processing technique.

**Modeling**

Accuracy table which contains the best accuracies that were estimated while **training** the model

| Model                  | Accuracy |
|------------------------|----------|
| RandomForestClassifier | 0.816    |
| ExtraTreesClassifier   | 0.812    |
| XGBClassifier          | 0.745    |
| CatBoostClassifier     | 0.807    |
| Ensembling             | 0.816    |

Ensembling with Randomforestclassifier and Extratreesclassifier had been used as the model in _ML_PumpItUp_BestScore.ipynb_ file which generated the best score.

The GridSearchCV had been used for hyperparameter tuning.

Go through the code for getting a better idea.

**Proof of Submission**

![Proof of Submission](https://user-images.githubusercontent.com/47107946/133722866-54e52445-0b0a-42bb-a972-c5dcb9f2bc56.png)


_Happy Coding!_
