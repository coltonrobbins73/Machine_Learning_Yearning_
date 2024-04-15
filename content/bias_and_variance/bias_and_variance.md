+++
title = 'Practical Considerations for Bias and Variance'
date = 2024-04-06T22:13:25-07:00
draft = false
+++

**Bias** : an algorithm's error rate on the training set. As the prediction model becomes more flexible to the training set the bias will go down.

**Variance** : an algorithm's error rate on the test set. A balance between flexibility and rigidity allows for the best generalized model. As bias approaches zero variance will increase dramatically due to overfitting.

#### Comparing bias and variance

Choosing an improvement strategy for your model can be challenging. One method for more focused optimization is to look at the bias and variance. Variance will usually be greater than bias because the model has not directly interacted with the test set. If there is a low discrepancy between bias and variance but your bias is still very high, you will be more successful in trying to improve bias and then trying to translate those gains into improvements in variance.

Here are some possible scenarios :

|           | High variance                  | Similar variance to bias |
| --------- | ------------------------------ | ------------------------ |
| High bias | Overfitted and underfiitted :( | Underfitted              |
| Low bias  | Overfitted                     | Good performance :)      |

#### Optimal error rate

The maximum performance you can achieve is called the optimal error rate, aka the Bayes error rate. For tasks that can be accurately performed by humans, the optimal error rate can be close to zero, while more complicated tasks can be difficult to determine. In all cases, however, it is advantageous to approximate the unavoidable bias to inform your decisions on how much improvement can be expected from the algorithm. If the training set is already close to the optimal error rate, you will be more successful in working on improving variance.

#### Solutions for error rate problems

###### High avoidable bias?

1. **Increase the size of your model** such as by adding extra layers to a deep neural network. This effectively makes the model more flexible or sensitive to the training set. 
2. **Create an eye training set** similar to what we described earlier for the eye dev set. Manually look through the misclassified training set examples and categorize the kind of errors that are being made in an analysis table. The table will help you pinpoint specific areas that can be improved on or identify additional features that should be incorporated into the model.
3. **Reduce regularization** from your model which gives more weight to individual features in the model.

###### High variance?

1. **Increase the amount of data for your training set.** This will increase the generalization of the training set to accommodate different use cases.
2. **Add regularization** to your model which dampens the fitting effect of certain model features. Regularization will be explained in more detail in subsequent chapters.
3. **Early stopping** reduces the amount of learning that occurs from the training set.
4. **Feature selection** to reduce some of the model features entirely. Recent computational advances typically allow for features to be modulated automatically by the algorithm but smaller datasets can still benefit from more aggressive feature selection.
5. **Decreasing the model size** will allow for less fitting to the training set. However, this technique is often unfavorable when compared to other available techniques.

###### Solutions for both bias and variance

1. **Modify input features** using insights gained from error analysis. Choosing the correct relevant input features can have a dramatic impact on outcomes.
2. **Modify the model architecture** entirely to better encapsulate the phenomenon that you are studying.

*Note that you will inevitably be limited by the amount of data you can collect and the scale of your ML model so resource use needs to be factored in when applying data and model depth modifications.


