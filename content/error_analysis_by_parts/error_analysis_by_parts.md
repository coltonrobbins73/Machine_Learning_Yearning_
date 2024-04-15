+++
title = 'Error Analysis by Parts'
date = 2024-04-07T17:57:43-07:00
draft = false
+++

Attributing error to the correct component of an algorithm is important for prioritizing optimizations. Workflows are ordered in a directed acyclic graph (DAG) with early components feeding processed data into later components. If an early component performs poorly, later components will likely perform poorly as well so it can be difficult to properly attribute error if the output is incorrect.

### Correcting outputs

To properly test each component carry out error analysis as described previously and identify all the misclassified examples from the algorithm. For each misclassified example, manually verify the output of each component. If at any point a components output is incorrect, simply provide a corrected perfect output to see if the next component can perform well enough.
