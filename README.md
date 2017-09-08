# Santander Customer Satisfaction Challenge                    


![Image](https://github.com/darshanbagul/Santander_Customer_Satisfaction/blob/master/images/santander.png)

Which customers are happy customers?

## Introduction
The goal of this competition was to predict if customers are satisfied or dissatisfied with their banking experience. The kaggle link to this competition can be found [here](https://www.kaggle.com/c/santander-customer-satisfaction)

## Dataset

We have an anonymized dataset containing a large number of numeric variables. The "TARGET" column is the variable to predict. It equals 1 for unsatisfied customers and 0 for satisfied customers.

The task is to predict the probability that each customer in the test set is an unsatisfied customer.

   1. train.csv - the training set including the target
   2. test.csv - the test set without the target
   
## Gradient Boost

Before tackling the challenge, it is important to understand the Gradient Boosting algorithm briefly. Gradient boosting is one of the most powerful techniques for building predictive models and has seen a massive rise in its use, before the success of deep learning models. A quick analysis of past Kaggle challenges, gives an insight into the usefulness of this class of Machine Learning models. A majority of Kaggle winners used some form of ensemble models, with Gradient boosted trees leading the pack.

The idea of boosting came out of the idea of whether a weak learner can be modified to become better. A weak hypothesis or weak learner is defined as one whose performance is at least slightly better than random chance. The first realization of boosting that saw great success in application was **Adaptive Boosting or AdaBoost**. The weak learners in AdaBoost are decision trees with a single split, called decision stumps for their shortness. AdaBoost works by weighting the observations, putting more weight on difficult to classify instances and less on those already handled well. New weak learners are added sequentially that focus their training on the more difficult patterns. 

**Predictions are made by majority vote of the weak learners’ predictions, weighted by their individual accuracy.** This is also referred to as **ensembling method**, where a majority vote is taken over different models for deciding the final prediction.

Gradient Boosting algorithm is a generalization of the AdaBoost algorithm. Gradient boosting involves three elements:
   1. A loss function to be optimized.
   2. A weak learner to make predictions. (Usually decision trees or regression trees)
   3. An additive model to add weak learners to minimize the loss function. (Trees are added one at a time, and existing trees in the model are not changed.A gradient descent procedure is used to minimize the loss when adding trees.)

Gradient boosting is a greedy algorithm and can overfit a training dataset quickly. Hence regularization is important for the algorithm to generalize well. Different regularization methods are deployed, such as:
   1. Tree Constraints such as limiting number of trees, depth of the trees, observations per split, etc.
   2. Weighted updates of the trees
   3. Random sampling
   4. Penalized Learning techniques such as using L1/L2 regularization on the leaf weight values of the trees.
   
  
## Implementation

We preprocess the dataset by eliminating features that do not contribute enough to the output variable. Then we split the dataset into train set and validation set. We train a simple logistic classifier as a base model for the task, and then implement as Gradient-Boosting Trees Classifier to try and improve the performance.

## Results

### Logistic Classifier
      AUC - 0.787

      Confusion Matrix
      +--------------+-----------------+-------+
      | target_label | predicted_label | count |
      +--------------+-----------------+-------+
      |      0       |        1        |   14  |
      |      0       |        0        | 14484 |
      |      1       |        1        |   2   |
      |      1       |        0        |  634  |
      +--------------+-----------------+-------+

### XGB Trees

      AUC - 0.98799871210328583
      
 As can be determined by the performance metrics, XGB Trees improve the model performance massively when compared to a simple logistic classifier.
 
The model can be further improved by implementing regularization and hypertuning XGB parameters. The model submission achieved a **score of 0.8423 on the Kaggle leaderboard** and was ranked at 730th place out of 5123 participants.
