# Autonomous precision error measurements
Yes, algorithms/robots can autonomously measure their own error. But there a lot of interesting caveats. This is not magic but a sophisticated version of error-correcting codes applied to the problem of measuring statistics of ground truth autonomously. The math of the algebraic approach advocated here (there are other methods based on maximum likelihood) has advantages and weaknesses.
* You cannot measure the accuracy error, only precision error.
* But this is not so bad because precision error is the hardest to manage anyhow.
* You require multiple sources of information.
* But this is not so bad in a world with many excellent alternatives for carrying out classification and regression tasks.
* Unlike maximum likelihood methods, the algebraic method comes with solution guarantees.

## Autonomously measuring your precision error in one-dimensional regression
The ICML 2008 paper -[Autonomous Geometric Precision Error Estimation in Low-Level Computer Vision Tasks](http://icml2008.cs.helsinki.fi/papers/121.pdf) - carries out autonomous precision error measurement for a single continuous variable. The result should be generalizable to multiple dimensions.
## Autonomously measuring binary classification error
Self-driving cars contain multiple components to detect different entities in its line of sight. Pedestrians, road signs, traffic lights, etc. Modularization of the software has lead to separate systems for, say, detecting pedestrians. Measuring the pixel tagging accuracy of a pedestrian detecting system using the binary classification ground truth inference algorithm is an example of a robot measuring its own error.

These are just two examples. There are many more to be found. Since you can only measure statistics of ground truth, there would be different algebraic systems for each statistic you want to measure.