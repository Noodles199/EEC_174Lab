# Lab 2: Written report questions

Answer the following questions in your written report. For questions about model performance, refer to results from your own notebook and report the relevant metrics.

## 1. Data and labels

1. **Prediction task:** What does one row of the dataset represent? What are the three classes predicted in this lab, and how are they constructed from the BSA and DTA annotations?

Answer: each row of dataset represents one breath cycle from a patient. The three class are non-PVA(0), Breath Stacking Asynchrony(1), and Double Trigger Asynchrony(2). The labels are created using the BSA and DTA annotations. If both are 0, the breath is labeled as non-PVA. If BSA is 1 and DTA is 0, it is labeld as class 1. If DTA is 1 and BSA is 0, it is labeld as Class 2.

2. **Ambiguous labels:** The notebook removes breaths annotated as both BSA and DTA. Why are these rows a problem for the three-class target? Describe one alternative to removing them.

Answer: Because the model uses three mutually exclusive classes, so each breath should have only 1 label. When both annotations are 1, the formula produces 3, which does not belong to any valide classes. One alternative is to use a multilable for classification, where a breath can have both BSA and DTA labels instead of mkaing it into only one class.


3. **Patient identifiers:** Why are `patient` and `breathid` excluded from the model inputs? Does excluding them guarantee that the model will generalize to patients it has never seen? Explain.

Answer: The two inputs are identification information, not actual breathing measurements. Inclluding them may cause the model to memorize patterns associated with specific patients or breaath IDs instead of learning useful breathing featrues. Removing the two columns does not guarantee that the model will generalize to new patients, becuase breaths from the same patient might still appear in both the training and validation sets.

## 2. Features and preprocessing

4. **Feature extraction:** Why does the lab extract features from flow and pressure waveforms before training a classifier? Identify two features that capture different aspects of a breath, and explain what each contributes.

Answer: because these measurements summarize important characteristics of each breath and make the data easier for a classifier to process. FOr example, tve_tvi_ratio is the ratio of exhaled air to inhaled air volume, which helps identify br4eath stacking. Another feature is e_time, which measures how long a patient exhales and can help identify double triggering ( when exhalation time is unusually short).

5. **Feature scaling:** Which scaling method did you use? Why should it be fitted on the training data and then applied to the validation data, rather than fitted on both datasets together?

Answer: I used standardscalar in task 2 to standardize the features. The scalar was fitted on the training data using fit_transform() and then applied to the validation data using transform(). This is crucial because fitting the scalar on both datasets would allow information from the validation data to influence preprocessing(data leakage). 

## 3. Model performance

6. **Random forest:** In your own words, how does a random forest combine decision trees to make a prediction? Give one reason it is a reasonable choice for this dataset.

Answer: A Random forest combines multiple decision trees to make predictions. Each tree is trained using a random sample of the training data and take random subsets of features into account when splitting. To classify, each tree predicts a class, and the forest uses majority voting to make the final prediction. It is a reasonable choice because it can handle multiple breathing features and learn complex relationships between them in which we don't need to determine classifciation rules manually.

7. **Class-specific errors:** Examine your random forest's classification report. Which class has the lowest recall, and what kinds of mistakes does that indicate? Why might accuracy alone hide this problem?

Answer: The class with the lowest recall is DTA(class2). Average recall is only 0.024. This means the model correctly identifies only about 2.4% of actual DTA, and most DTA are wrongly classfied as other classes. Accuracy can hide this because the dataset is imbalanced, with many more non-pVA and BSA breaths than DTA breaths. The model can still obtain high accuracy by corcctly classifying these majority classes.

8. **Precision and recall:** For detecting BSA or DTA, what is the difference between a false positive and a false negative? Explain a situation in which you would prioritize recall over precision for one of these classes.

Answer: False positive: when the model predicts that a breath is BSA or DTA, but the breath does not actually belong to that class. False negative; a breath actually belongs to BSA or DTA, but the model fails to detect it. I would prioritize recall when detecting DTA because missing a double trigger event could be more concerning than incorrectly flagging a normal breath. HIgher recall helps identify more actual DTA cases, although it may also increase false positives.

9. **Model comparison:** Compare the random forest with the other supervised-learning model you implemented. Which has the higher F1-score? Does the same model perform best for every class? Support your answer with your results.

Answer: I compare random forest with KNN classifier. Based on my results, Random Forest performed better, with a macro F1-score about 0.66264, compared with 0.5 for kNN. Random Forest and lower misclassfication rate of 0.1143, compared with 0.3336 for kNN. 

## 4. Model selection and validation

10. **Feature selection:** Compare performance using all available breath features with performance using selected features or the lab's expert-defined rules. Did the reduced feature set improve validation performance? Why might a feature that appears useful on the training set fail to improve validation performance?

Answer: The expert feature selection method achived an accuracy of 0.9, and a macro F1-score of 0.77 on the training set. It performed well on non-PVA and BSA, with F1-scores of 0.96 and 0.88, but had a lower F1-score of 0.47 for DTA. The results can't tell us if reducing the feature set improved validation perforamnce, because he expert-rule method was evaluated on the training data, while the Random Forest was evaluated on validation data. To make a fair comparison, both methods should be evaluated on the same validation set.

A feature seems useful on the training set may not improve validation performance because it might capture patterns specific to the training data rather than patterns that generalize to new breaths. This is overfitting. 

11. **Cross-validation:** What does stratification preserve in 5-fold cross-validation? Report your F1-score for each fold and its average. What would substantial differences between folds suggest?

Stratification means keeping about the same proportion of each class in every fold as in the original dataset. My macro F1-scores across the five folds were reltatively consistent ( around 0.92, they were 0.9194, 0.9266, 0.9123, 0.9224, and 0.9250 respectively).  This means that the model's performance was stable across these different training and validation splits. If the scores differed substantially, it could indicate that the model is sensitive to the data split. 

12. **Patient-level validation:** If breaths from the same patient appear in both training and validation sets, how might that affect the reported performance? Describe a validation strategy for estimating performance on patients the model has not seen before.

Answer: The model can learnn patterns specfic to that patient instead of general breathing patterns if that happens. SInce both training data and validation data ahs the same breath, this might make the validation performance appears to be better than generalizing to a new patients. 

A better way is to split the dataset by patient rather than by ndividual breath. For example, we group patients instead of grouping the variables. This can help us to evaluate how well the model performs on new patients.
