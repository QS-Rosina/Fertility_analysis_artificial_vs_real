# Fertility_analysis_artificial_vs_real
This study examines the relationship between lifestyle-related factors and fertility outcomes in two distinct datasets: a couples dataset that focuses on pregnancy success and a semen quality dataset.

Using data preprocessing, Unsupervised Random Forest (URF) analysis, Random Forest classification, feature importance, and cross-dataset prediction, the study investigates the similarities and differences across the datasets.

The primary goal is to determine whether the artificial dataset has predictive power on real-world data.

The project addresses the following questions:
- Can lifestyle and demographic variables help distinguish between Normal and Altered semen quality?
- What patterns and similarities can be identified within the semen and couples datasets using Unsupervised Random Forest analysis?
- Which shared variables, such as age, smoking, and alcohol consumption, are most relevant to prediction?
- Can a model trained on one dataset predict outcomes in the other dataset?
- How well do these models generalize, and what are the limitations of transferring predictions between datasets?

## Data
The data used for this project came from KAGGLE:

### Couples artificial dataset
The target variable represents pregnancy success. The dataset is also used to explore patterns in the data and to test whether a model trained on semen data can generalize to a different population and outcome.

### Male-only real-world dataset 
The semen dataset contains demographic and lifestyle information alongside a semen quality outcome.

To enable cross-dataset comparisons, a subset of conceptually comparable variables is selected from both datasets. These include:

- Age
- Smoking habits
- Alcohol consumption

The data from the links are pre-cleaned.
The datasets do not contain matching individual identifiers and have different target variables. Therefore, they are analysed separately rather than merged at the individual level.

## Data preprocessing
After being cleaned, the datasets are ready for analysis. This entails choosing pertinent variables, dealing with missing values, and, when necessary, encoding categorical data into numerical representations.
In order to evaluate models trained on one dataset using similar input variables, the common features are aligned.

## Unsupervised Random Forest
The structure and similarity of samples within each dataset are examined using unsupervised Random Forest analysis.
Each feature is shuffled independently to create artificial data. Next, a Random Forest classifier is trained to differentiate between artificial and real observations. The fitted model is used to extract the proximity between actual observations.
After repeating the process, the proximity matrices that are produced are averaged. Principal component analysis (PCA) is used to analyze the average proximity matrix after it has been converted into a dissimilarity matrix.
A two-dimensional depiction of sample similarities and differences is given by the generated PCA plots.

## Random Forest Classification
Random Forest classifiers are used to predict semen quality and evaluate how well the available features distinguish between Normal and Altered samples.
Model performance is evaluated using cross-validation. Leave-One-Out Cross-Validation (LOOCV) is used for the semen dataset, where each observation is held out once while the model is trained on the remaining observations.
The main evaluation metric is the Area Under the Receiver Operating Characteristic Curve (ROC-AUC).

## Feature importance
Feature importance is investigated using permutation importance based on ROC-AUC.
This technique assesses how shuffling the values of a single feature affects the model's performance. A larger reduction in performance indicates that the model relies more heavily on that feature.
Feature importance is used to compare the relative predictive relevance of shared variables across the datasets.

## Cross-dataset validation
Transfer learning experiments are performed in both directions:
Couples → Semen: train a model on the couples dataset and evaluate it on the semen dataset.
Semen → Couples: train a model on the semen dataset and evaluate it on the couples dataset.

# Results and key findings
## Unsupervised Random Forest analysis
The URF analysis suggests that the degree of separation visible in the PCA plots differs between the datasets. For the semen dataset, the first principal component explains approximately 11.7% of the variation represented by the URF dissimilarity analysis, and the plot does not show clear separation between the outcome groups. For the couples dataset, the first two principal components together explain approximately 2.7% of the variation. The observed U-shaped pattern should be interpreted cautiously because the two-dimensional PCA projection captures only a small proportion of the variation.

## Predictive performance
Limited predictive performance is shown by the classification and transfer trials.
The LOOCV ROC-AUC for the semen model is roughly 0.59. ROC-AUC values of roughly 0.62 for Couples → Semen and 0.58 for Semen → Couples were obtained from cross-dataset experiments. With performance comparable to chance-level ranking (ROC-AUC = 0.50), these values show poor discrimination across outcome classes.

## Feature importance
In both datasets, age was found to be a significant predicting factor. Between the datasets, there were differences in the relative relevance of alcohol use and smoking.
These variations imply that the models do not find the same predicted patterns in the two datasets. Feature importance should be assessed carefully, though, especially in situations with small sample sizes.

# Overall interpretation
The results imply that common lifestyle and demographic factors offer little predictive value across different datasets. The models do not show great generalization from one dataset to another, despite certain similarities.

The poor transfer performance could be caused by variations in sample sizes, data distributions, outcome definitions, and demographic characteristics.

## Limitations
Several limitations should be considered when interpreting the results:
- Different outcomes: Semen quality and pregnancy success are related to fertility but are not equivalent outcomes.
- Different populations: The datasets represent different populations and may have different underlying relationships between features and outcomes.
- Limited shared features: Cross-dataset prediction is restricted to variables that can be meaningfully aligned between the datasets.
- Limited sample size: The semen dataset contains relatively few Altered samples, which can make performance estimates and feature importance less stable.
- Low predictive performance: ROC-AUC values close to 0.50 indicate limited ability to discriminate between outcome classes.
- Exploratory analysis: Observed associations and predictive importance do not establish causal relationships.

# Conclusion
This project assesses whether predictive models can generalize across semen and couples datasets and whether demographic and lifestyle patterns may be found within them.

While Random Forest classification and cross-dataset transfer tests evaluate predictive performance, URF offers an exploratory view of sample similarity. The findings show that a model trained on one dataset may not transfer well to another and that the shared features have limited predictive ability.

Overall, the results show how difficult it is to compare various fertility-related datasets and how crucial it is to take into consideration variations in demographics, factors, outcomes, and sample sizes.

# Technologies
- Python
- pandas and NumPy for data manipulation
- scikit-learn for Random Forest modelling, cross-validation, ROC-AUC, and permutation importance
- Matplotlib for visualisation

# Reproducibility
- Obtain the original datasets and place them in the appropriate project directories.
- Run the data-cleaning and preprocessing steps.
- Generate the shared-feature datasets.
- Run the URF analysis and PCA visualisations.
- Run the Random Forest classification and LOOCV evaluation.
- Calculate feature importance and perform cross-dataset prediction.
- Compare the resulting metrics and visualisations.

# Data availability
Both datasets can be found on Kaggle.
Male-only real-world dataset - https://www.kaggle.com/datasets/gabbygab/fertility-data-set 
Artificial couples dataset - https://www.kaggle.com/datasets/shauryasrivastava01/fertility-health-dataset
The couples dataset contains demographic and lifestyle information related to pregnancy outcomes.
