# Ground Truth Problems in Business
Collection of papers and presentations related to ground truth inference in data science
![Flammarion engraving](img/Flammarion.jpg)

The Flammarion engraving is frequently taken as a metaphor for piercing the veil of reality to understand what is really going on. The engraving also illustrates the goal of solving *ground truth problems* in business. In your company the ground truth of the production data stream may not be known. Or it could be hard to compute. Or private.

This collection contains examples of my work that solve the ground truth inference problem by estimating a statistic of ground truth without knowing ground truth itself.

The term *ground truth* sounds fancy and philosophical but it is not. It actually is easy to understand and it is just a generic term for the different forms it takes. Let's take one case I discuss here - binary classification. You have a bunch of data and each of your data points has an "A" or "B" label. The ground truth for that data would be the list of the true labels for each of the data points,
<a href="https://www.codecogs.com/eqnedit.php?latex=\{\ell_{i,\text{true}}\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\{\ell_{i,\text{true}}\}" title="\{\ell_{i,\text{true}}\}" /></a>.
Another example would be a company that sells speech recognition as a service to call centers. Ground truth could be the transcripts for all the audio it processed daily in production.

The way to get around the problem of not having ground truth is to realize that, for most business decisions, the role of ground truth is to allow a statistic of ground truth to be computed! Ground truth is used to compute the statistic and then "discarded"! So if you can estimate the statistic directly, you eliminate the problem of not having the ground truth.

## Decisions not Predictions
Business decisions are frequently driven by average or SLA performance. Not all output is expected to be perfect and statistics of the data are used to specify SLA agreements. The most accurate algorithm is measured in the aggregate with decision makers not wanting to get into the details of the performance. I never attended a meeting during my days in speech recognition where Word Error Rate (WER) was not the only metric used to select best production algorithm after all other engineering constraints were satisfied.

Marketing questions like what percentage of our users visited our publisher network more than once last month is another example of a business statistic of interest to decision makers. 

When your daily traffic consists of tens of millions of users, computing this statistic using your company's database is a nightmare. Not even a Spark cluster can handle daily visits for a month of data without taking days to spit out an answer.

A way to understand the difference between decisions and not predictions is to think about about examples like 
* I don't have to outrun the bear, just you.
* Top candidate needs to be selected
The above examples are connected to the issue of precision versus accuracy error in ground truth problems.
## Precision is expensive, accuracy is not
Another theme that comes up in ground truth problems is the distinction between accuracy and precision error. You have experienced this if you have tweaked a zeroing screw on a mechanical weight scale or used the focus on your camera. Accuracy is cheap and easy. Precision, good quality lenses that perform uniformly over the whole view field, is expensive. So, while ground truth inference algorithms cannot frequently measure your accuracy error, they can measure your precision error. Hence they give you insight on the hardest quality measurement of your company's product - its precision.