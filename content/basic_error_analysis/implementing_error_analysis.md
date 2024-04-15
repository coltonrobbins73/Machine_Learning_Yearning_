+++
title = 'Implementing Error Analysis'
date = 2024-04-05T20:15:44-07:00
draft = false
weight = 3
+++

Even experienced ML practitioners can struggle to pick the best strategy for a new project. Therefore, it is best to get something running quickly even if it is poorly optimized. Evaluating and attributing error in this initial system will be the best tool to narrow your focus in the correct direction.

#### Visual inspection of dev sets

For classification errors, it is useful to categorize the different kinds of errors using manual human review. A simple dev set of 100 misclassification examples can be examined quickly. If there is a specific kind of error that only occurs 5% of the time, it might not be the best focus point for improved optimization. Instead, try to find error patterns that are more ubiquitous in the misclassified dev set.

An example of this might occur as follows :

1. Manually look through 100 misclassification examples in a dev set.
2. For each image create a row in a table with columns corresponding to identified error patterns.
    - As you cycle through examples, new error categories will become apparent and can be added retroactively
    - Note that sometimes examples are misslabeled before being processed by the algorithm. If there is a significant numeber of mislabeled examples, add an error category column for this case as well.
3. Add up the percentage for each column
    - Note that a single example might match to multiple error categories so the total percentage might be more than 100

The final percentages will show you the hgihest priority tasks for your ML model and give you a rough estimate as to how much improvement you can expect from trying to correct each error category

#### Misclassified examples

As discussed previously, if the percentage of misclassified examples is low than it is much lower priority to address them. If the percentage is high, it might be worth the effort to relabel the dev set. Ensure that your relabeling mehtod is also applied to the test set so the data is uniform throughout. Finally, make sure you review correctly classsified examples for mislabeling errors not just the misclasified examples.

#### Splitting technique for large dev sets

If you have thousands of examples in your misclassified dev set, it would be impractical to manually review each one. Splitting the dev set into an **eye dev set** and a **black box dev set** can help alleviate this problem. The eye set will contain a small proportion of the misclassified examples (maybe 10%) to be used for error categorization. The black box set will contain the majority of the misclassified images to be used for parameter tuning. Make sure you evaluate both the eye and black box set seperately as overfitting to the eye set is common because you have hands-on intuition from looking directly at this set. If eye set performance increases at a much faster rate to black box set, you need to add more data to the eye set or get entirely new labelled data.

#### How big should eye and black box sets be

The size of the eye set is determined by the error rate of your algorithm. Here are some general rules for absolute error numbers :

- 10 errors : very limited information making error pattern identificaiton very difficult. Only acceptable if you have very limited data and you need to withold as little as possible from the black box set
- 20 errors : slightly better information allowing you to get a rough sense of error patterns
- 50 errors : good information allowing much better understanding of error patterns
- 100 errors : very good information allowing very good error pattern recognition

You can manually check many more examples as long as you have enough data for optimizing parameters. Time constraint limits are a factor here so typically people do not manually analyze more than 500 errors.

Taking absolute numbers into account, if your algorithm has a 5% error rate and you want 100 errors to manually view you would need 2,000 examples reserrved for the eye set. When your error rate is low you will need a larger eye set to get a sufficient number of errors to manually evaluate.

For the black box set, the optimal number of examples is between 1,000-10,000 but more data is almost always better. However, if you are data starved, the eye set is usually more important and so it is acceptable to use only an eye set for error analyses, model selection, and hyperparameter tuning. However, using only an eye set increases the risk of dev set overfitting.

#### Comparisons to human-level performance

Frequently, machine learning is designed to automate tasks that are regularly performed by humans. By including information on human performance, ML algorithm development can be greatly improved.

1. **High accuracy labeling** allows for a robust ground truth.
2. **Human intuition** can be factored into the learning process by incorporating additional information that humans regularly use to solve specific problems.
3. **Optimal error rate is known** and can be used for accurate goal-setting and optimization prioritization.