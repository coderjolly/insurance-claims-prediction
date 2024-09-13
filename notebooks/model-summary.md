## Model Performance Summary

1. Data Processing Steps
   - Handling Class Imbalance: The target variable (Response) exhibited significant class imbalance, with a majority of "0" (no claims)   compared to "1" (claims). Different strategies were employed to handle this imbalance:

        - Baseline Notebook: Models were developed without addressing class imbalance.
        - Oversampling Notebook: Used Synthetic Minority Over-sampling Technique (SMOTE) to balance the dataset by creating synthetic samples for the minority class.
        - Undersampling Notebook: Used NearMiss2, an undersampling technique that selects the majority class samples closest to the minority class, balancing the dataset by reducing the majority class.

    - Data Preparation: Feature scaling and encoding were applied where necessary. Categorical features were one-hot encoded, and numerical features were scaled using StandardScaler or MinMaxScaler. Columns with symbols < and > were renamed for compatibility with machine learning models like XGBoost.

2. Model Development
   - Model Selection: Three machine learning models were primarily used across all notebooks to evaluate the effectiveness of different sampling techniques:
          - Random Forest Classifier
          - XGBoost Classifier
          - LightGBM Classifier
   - Hyperparameter Tuning:Each model underwent hyperparameter tuning using RandomizedSearchCV to optimize performance. The `Model_Driver_Function` was employed to "Perform train-test splits", "Tune models using randomized search", "Generate classification reports", "confusion matrices", "ROC", "Precision-Recall curves" and "Save model states for future use".
   - Evaluation Metrics: Models were evaluated using several metrics:
        - Accuracy, Precision, Recall, F1-score
        - ROC AUC Score
        - Precision-Recall AUC Score
        - Confusion matrices were generated for both training and testing sets to analyze true positives, false positives, true negatives, and false negatives. 

3. Model Evaluation/Performance
    - Baseline Notebook: The baseline models without addressing class imbalance performed poorly, with the Random Forest Classifier achieving the almost "No Skill" ROC AUC score of 0.5.
        - Random Forest: High precision but poor recall for the minority class ("1"), leading to a low F1-score.
        - XGBoost: Improved recall for the minority class but still limited in generalization.
        - LightGBM: Provided the best balance between precision and recall for the minority class but still showed limitations due to the class imbalance. 
    - Oversampling Notebook (SMOTE): The models trained on the oversampled dataset showed significant improvements in performance metrics compared to the baseline models.
        - Random Forest: Balanced precision and recall after oversampling, with a notable improvement in minority class prediction.
        - XGBoost: Performed well with balanced precision and recall, achieving an AUC score over 0.84 on both training and testing sets.
        - LightGBM: Showed the best performance with the highest AUC and F1 scores among all models, demonstrating its effectiveness in handling balanced datasets.
    - Undersampling Notebook (NearMiss2): The models trained on the undersampled dataset showed mixed results compared to the oversampling models, had to use version 1 because of low computational power.
        - Random Forest: Showed reasonable recall for the minority class but suffered in precision due to the reduction in majority class samples.
        - XGBoost: Similar results to Random Forest with some improvement in F1 scores.
        - LightGBM: Performed best among the models after undersampling, but still showed limitations compared to oversampling results.

4. Rationale for Model Selection
   - Random Forest: Chosen for its simplicity and robustness, providing a quick baseline for comparison.
    - XGBoost: Selected for its efficiency and capability to handle large datasets and complex patterns. It allows for better control over regularization and model complexity.
    - LightGBM: Chosen for its speed and performance, especially with large and imbalanced datasets. It showed superior results in handling balanced datasets created using SMOTE.
  
5. Limitations of the Analysis
   - Computational Costs: The biggest limitation for me was that techniques like SMOTE and hyperparameter tuning using RandomizedSearchCV can be require significant processing time and resouces and I didn't have access to a GPU.
   - Class Imbalance: The original dataset's significant class imbalance posed a challenge. While oversampling improved recall for the minority class, undersampling reduced the precision due to fewer samples.
   - Model Overfitting: There is a risk of overfitting in oversampled models due to synthetic data. Conversely, undersampled models might underfit due to the reduced training data.
   - Some feature engineering could have been done to improve model performance, such as creating new features or combining existing ones to capture more information but unfortunately I didn't have the time to do this. 

6. 
