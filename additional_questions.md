### Tell us how you validate your model, which, and why you chose such evaluation technique(s).

1. First, split dataset into (A) train and (B) validation sets - the validation set will only be used to evaluate the performance of the model after it has been tuned.
2. Next, evaluate the model on the (A) train set using K-folds cross validation - this ensures that the model training performance is not over-fitted and works well with a random scenario (mimics real life).
3. After param tuning, evaluate the model on (B) validation set to get an idea of how well the model performs on an unseen set of data.

### What is AUC? Why do you think AUC was used as the evaluation metric for such a problem? What are other metrics that you think would also be suitable for this competition?

AUC is the Area under Receiver Operating Characteristic (ROC) curve. It shows the trade-off between the True Positive Rate and False Positive Rate.
AUC is a good measure of how close the predicted probability is to the actual labels, and is preferred compared to other metrics like accuracy, recall, and precision, which take a binary-view on the predictions. In this problem, since the actual probability is more important than the class prediction, AUC is an ideal metric. 

Other metrics: F1-score, Recall, Precision.
That said, using F1-Score, recall, and precision could also help to get a gauge on how well the model can differentiate between the 2 classes. To decide which metric to use, we need to ask the following questions: Which is more important - being able to capture all persons with high probability? Or ensuring that nobody is wrongly accused of having a high probability? The use-case and business actions/plans for the model would help us to understand which metric to use. For example, if the model were to be used for bank staff to identify people to deny loans to, being able to capture all persons with high probability is more important. In this case, optimising Recall would be helpful. However, if it were to be used for consumer to self-evaluate their financial outlook, ensuring that they are not wrongly accused of having a high probability is more important, since they could be making huge decisions (e.g. buying a home, preparing for marriage) based on the outcome. In that case, optimising Precision would be more useful.

### What insight(s) do you have from your model? What is your preliminary analysis of the given dataset?

From the feature importances, we can tell that:
-  Whether a person experienced 90 days past due delinquency or worse is highly related to their historical record of late payments and their age-group, which could be indicators of their tendency and ability to pay.
- It is also highly related to their RevolvingUtilizationOfUnsecuredLines (Total balance on credit cards and personal lines of credit except real estate and no installment debt like car loans divided by the sum of credit limits.), which might be an indicator of their debt situation and spending habits.
- The NumberOfDependents and real estates are not strong features, possibly because there is a circular-relationship between the 2 features and the target feature (e.g. the more income you have to spend, the more real estates you will purchase. The more real estates you purchase, the more loans you have.).

Based on the data exploration, we know that positive cases usually:
- Are between the age 20-40.
- Have more number of late days previously
- Have slightly lower number of credit lines and loans
- Have slightly lower number of real estate lines and loans.

### Can you get into the top 100 of the private leaderboard, or even higher?
Haha ;) Possibly yes, if I try out a different model (XGB/LGBM) and spent more time engineering better features.