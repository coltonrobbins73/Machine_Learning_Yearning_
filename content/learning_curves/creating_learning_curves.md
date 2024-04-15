+++
title = 'Creating Learning Curves'
date = 2024-04-07T01:28:16-07:00
draft = false
+++

Learning curves are a graphical representation of the output of some continuous function related to algorithm performance. For instance, we can plot dev set error percentage as a function of training set size.

For example, as training set size increases, we can expect dev set error to decrease. Identifying the global maximum of this graph will identify the optimal training set size

![Error vs training set size](/machine_learning_yearning/images/error_vs_training_set_size.jpg?classes=left)

## Interpreting learning curves

###### Plateau regions

Plateau regions will not benefit from further increases in training set size. In this graph, the optimal training set size is just before the plateau at what is called the elbow point.

![Error plateau](/machine_learning_yearning/images/error_plateau.jpg?classes=left)

###### Including training error

When the training set size increases, the training error should increase because we are introducing more variability into the training set data and thus it is more difficult to fit a trend to noisier data. 

![Including training error](/machine_learning_yearning/images/dev_and_train_error_vs_training_set_size.jpg?classes=left)

###### High avoidable bias

When there is a small discrepancy between dev and training error, we know that we cannot improve performance by better generalization to the dev set. Thus, adding more data to the training set will not improve dev set performance.

![High avoidable bias](/machine_learning_yearning/images/high_avoidable_bias.jpg?classes=left)

###### High variance

When there is a large discrepancy between bias and variance and bias is almost optimal, there is likely some overfitting occurring which can leak performance. Therefore, adding more data to the training set will gradually increase dev set performance.

![High variance](/machine_learning_yearning/images/high_variance.jpg?classes=left)

###### Noisy learning curves

When data is scarce, your learning curve subsets might not accurately capture the distribution of the complete data set. When this happens, the smaller training set sizes can be highly variable and will therefore hinder your ability to see data trends in the resulting graph.

Here are some solutions for this scenario :

1. **Consider bootstrapping** your data by sampling your data with replacement. Measure the error produced from each sampling and then take the average error to get a more accurate representation of the true distribution of the data.
2. **Use a balanced subset** of the data which forces accurate representation of unique classes. For instance, if your data has only a few positive examples, say 10%, force each subset to contain around 10% positive examples.
