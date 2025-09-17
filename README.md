Placement Prediction using Machine Learning

This project is an end-to-end Machine Learning pipeline to predict whether a student will get placed based on their CGPA and IQ score.


Project Workflow

Data Collection – Placement dataset (modified_placement_data.csv)
Data Preprocessing & EDA
Checked missing values, datatypes, shape of dataset
Scatter plot of CGPA vs IQ with placement labels
Feature Selection – Selected CGPA and IQ as input features, Placement as output label
Train-Test Split – Divided data into training (90%) and testing (10%)
Feature Scaling – Applied StandardScaler to normalize input features
Model Training – Trained a Logistic Regression classifier
Model Evaluation – Calculated accuracy score on test data
Visualization – Plotted decision boundary of the trained model
Model Deployment Ready – Saved model as model.pkl using Pickle

Programming Language: Python
Libraries: Pandas, NumPy, Matplotlib, Scikit-learn, Mlxtend, Pickle
IDE/Notebook: Jupyter Notebook / VS Code


Results
The Logistic Regression model achieved good accuracy on the test data.
Decision boundary visualization clearly shows the separation between placed vs not placed students.


Future Improvements
Try other algorithms (Random Forest, SVM, XGBoost)
Add more features (communication skills, projects, internships, etc.)
Deploy model using Streamlit / Flask for web-based prediction

Sample Output
Scatter plot (CGPA vs IQ)
Decision Boundary plot (Logistic Regression)

