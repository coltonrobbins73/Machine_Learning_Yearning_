+++
title = 'Practical Considerations of Data Combination'
date = 2024-04-07T05:27:25-07:00
draft = false
+++

Data collection is widespread among countless different entities resulting in a varied collection of different data distributions even within very similar categories. Combining data from different sources can dramatically increase the capabilities of an ML model. However, using data from multiple sources can conflict with the previously stated rule of keeping data distributions consistent across sets. Here, we explore options for combining data from different distributions which might contain different features.

### Training set vs dev/test set data distribution

It is recommended to only use data you expect to encounter in future problems for dev and test sets. If you have extra data that is not perfectly relevant but still might benefit your algorithm, it is best to restrict this extra data to the training set but still divide the most relevant data evenly among the training and dev/test sets.

### Should you incorporate extra data into your training set?

This depends on how closely the extra data matches with your dev/test set data and how much compute resource you have access to. When you add extraneous data to your training set the following effects occur:

1. Your ML model has access to many more examples and can learn from some of the similarities between the different types of data.
2. The ML model will expend some of its capacity to learn about properties that are only specific to the extraneous data.

If you have enough compute capacity, the second point is less impactful on your decision. Therefore, if the extra data has enough similarity to your original data, it might be beneficial to add it to the training data set because there might exist some model that works for both types of data. This is especially true for modern model architectures which are generally more flexible and powerful.

### Weighted data

If you have resource limitations but want to include additional data, you can use a weighting factor to limit the influence of the additional data. The weighting factor can be tunable based on how much divergence there is between the dev/test set and the additional data distribution as well as the availability of the different data types. For instance, if you have 50x more additional data as compared to the original data, you might need to use a more aggressive weighting factor to make sure the model is not over-influenced by the additional data.

### Data mismatch

If you observe your algorithm has high error on the dev/test set, there could be three general reasons for this :

1. Poor training set performance or high bias.
2. Poor generalization ability to the dev/test set or high variance.
3. Good generalization to unseen data from the training set but not to the dev/test set distribution aka **data mismatch**.

To identify data mismatch, you can split your training set into two subsets.

1. **Training set** that is seen by the algorithm.
2. **Training dev set** that is not seen by the algorithm but with the same distribution as the training set.
3. **Dev and test sets** that are drawn from the data distribution that is most relevant to the problem we are working on.

### Solutions to data mismatch

When you encounter a data mismatch scenario you should do the following :

1. Try to understand the most important differences between the different types of data and why they might be affecting your performance in different contexts.
2. Try and find additional data that more closely matches the dev/set data distribution.
3. As a last resort, you can remove a portion of the data from the training set.

### Synthesized data

When more data is needed for your model, one option is to simulate additional data. For example, if you have a speech or image recognition program that struggles with distorted information you can artificially distort real data to generate more examples for the ML model. Care should be taken with this strategy as the methods used in synthetic data generation can be overfit to. For example, if you add motion blur to a set of images using a defined function, the true randomness of real-world motion blur might not be accurately captured and thus your algorithm would perform poorly on more nuanced real-world data. Deciding on the suitability of simulated data depends on many factors and should be determined on a case-by-case basis.