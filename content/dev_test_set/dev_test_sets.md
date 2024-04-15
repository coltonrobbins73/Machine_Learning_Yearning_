+++
title = 'Developement and Test Sets'
date = 2024-04-03T20:57:31-07:00
draft = false
weight = 3
+++

When you have a set of data it is important to randomly distribute it into different sets to train and then evaluate the model. 

- **Training set** : makes broad changes to the ML model through backpropagation. Usually 60% of the data withheld.
- **Development set** : evaluates model performance and makes more minor changes to the hyperparameters of the model like the number of layers or learning rates.
- **Test set** : evaluates model performance but does not effect the model mechanics in any way.

The dev and test sets are critical for directing your efforts for future modifications.

#### Selecting the right sets

- Make sure your data is representative of what you might get in the future or the model will suffer.
- Make sure your dev and test set come from the same distribution. This can reduce some confounding factors like dev overfitting.

#### Optimal size of dev/test set?

Set size should correlate with the effect size you wish to detect. If you are trying to capture very minute performance gains between different algorithms (e.g 0.1%) you will need a large set size. A typical range is from 100 (very small) to 10,000 (moderate) to millions or billions (large). Typically, 1,000 - 10,000 is enough to see a difference of 0.1% in terms of performance. Note that as big data trends increase, set sizes are getting smaller with the majority of the data being used for training.

#### Single-number evaluation

Model performance evaluation can be simple or complex. Given this spectrum, development will progress better if you choose a single-number evaluation metric to quickly rank strategies unambiguously. If you must use a more complex precision-recall evaluation metric, it is better to combine these values into a single metric using averages, weighted averages, or an F1 score.

#### Satisfying evaluation strategy

When comparing multiple evaluation metrics that are not easily averaged it helps to maximize just one metric (optimizing metric) and evaluate other metrics on a threshold basis (satisfying metric). For example, run time is not very comparable with accuracy but in reality, we can tolerate a range of run times that meet a reasonable threshold value but we really want to maximize every bit of the accuracy. This kind of focus can greatly improve the development time for an ML model.

#### Speeding up iterations

You will almost always go through several iterations to find an optimal ML solution for a given problem. The quicker you can evaluate incremental gains in your iterations, the faster your development will progress. Therefore it is imperative to have clearly defined simple evaluation metrics on repeatable dev sets.

#### When to change dev/test sets and metrics

Typically with new projects, it is better to quickly put together dev/test sets and metrics that may not be perfect to start working towards a goal right away. However, when the initial evaluation metrics and sets are not performing it is best to rapidly pivot to something.

Some possible causes for incorrectly ranking classifier strategies

1. The real-world distribution of data is different than your dev/test set. 
    - **Solution** : get better data.
2. You have overfit to the dev set. This will be apparent if your dev set is substantially outperforming your test set. You can track progress by continually running the test set but you should not use test set evaluations to modify the algorithm in any way. 
    - **Solution** : get a fresh dev set.
3. The current metric is not optimal for the project's true goals
    - **Solution** : come up with a new metric or series of metrics that accurately capture the intended goal of the project.

