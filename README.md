# Heart_disease
Step 10: Model Limitations and Real-World Considerations
Limitations of This Analysis
Small Dataset (303 rows): Real clinical models need thousands of patients to be reliable.
Our results may not generalize well to new patient populations.

Cleveland Dataset Only: This data is from one hospital in Cleveland, USA.
Heart disease patterns may differ across ethnicities, regions, and ages.

No Cross-Validation: I used a single 80/20 split. In practice, K-Fold cross-validation
gives a more reliable estimate of model performance.

Binary Target: The original UCI dataset has 5 levels (0 = no disease, 1-4 = severity).
I converted to binary (0 vs 1-4). This loses severity information.

Feature Engineering: We could create new features (e.g., age groups, cholesterol ratio)
that might improve predictions.

Is This Model Ready for Clinical Use?
No. This is a learning exercise. A model for real clinical decision support would require:

External validation on independent patient cohorts
Review by cardiologists
Regulatory approval (FDA in USA)
Explainability for doctors (why did it predict disease?)
Step 11: Summary and Key Findings
Dataset
303 patients, 13 features, binary target (heart disease: yes/no)
Dataset was roughly balanced (54% disease, 46% healthy)
Minor missing values in ca and thal — filled with median
Preprocessing Decisions
Encoding: One-hot encoding for multi-class categoricals (cp, restecg, slope, thal)
Outliers: Kept — extreme values in medical data are clinically meaningful
Scaling: StandardScaler — simple, effective, no distortion
Box-Cox avoided — it produced extreme values (thalach: 16654) due to bad lambda fitting
Model Results
Model	Accuracy	F1-Score	Notes
Logistic Regression	~85%	~85%	Good baseline, interpretable
Decision Tree	~80%	~80%	Risk of overfitting at deeper depths
Random Forest	~85%	~85%	Best overall, feature importance available
KNN (optimal k)	~83%	~83%	k=1 overfit; best k found from analysis
Key Findings from Feature Importance (Random Forest)
thalach (max heart rate) — most predictive feature
cp (chest pain type) — strong indicator
oldpeak (ST depression) — third most important
ca (number of vessels) — significant predictor
age — moderate importance
Important Lessons Learned
k=1 in KNN is overfitting — it memorizes training data (100% train accuracy)
Box-Cox can fail badly — always check transformation outputs before proceeding
Recall > Accuracy in healthcare — catching sick patients matters more than overall accuracy
Feature importance must be computed and verified — not just claimed in summary
