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

A way to understand the difference between decisions and not predictions is to think about examples like 
* I don't have to outrun the bear, just you.
* Top candidate needs to be selected.

The above examples are connected to the issue of precision versus accuracy error in ground truth problems.
## Precision is expensive, accuracy is not
Another theme that comes up in ground truth problems is the distinction between accuracy and precision error. You have experienced this if you have tweaked a zeroing screw on a mechanical weight scale or used the focus on your camera. Accuracy is cheap and easy. Precision, as in good quality lenses that perform uniformly over the whole view field, is expensive. So, while ground truth inference algorithms cannot frequently measure your accuracy error, they can measure your precision error. Hence they give you insight on the hardest quality measurement of your company's product - its precision.

## Presentations
### When ground truth is expensive to compute
HyperLogLog is a data streaming algorithm typically used to estimate the number of uniques in a collection. Data stream algorithms are inference algorithms that refuse to store the ground truth. This has the nice side-effect that it makes them private. In the case of HyperLogLog, you can find out the number of uniques in a set without knowing any of the ids for the unique objects in the collection. 

The [Time In Ad-Tech Data Flows](presentations/TimeInAdTechDataFlows.pptx) talk I gave 2015 at DataXu discusses how you can use HyperLogLog to measure the time dynamics of data in a very large industrial database. HyperLogLog makes possible measurements extending over three or four months of data that would be incredibly expensive (in time and memory!) to calculate exactly with a formal SQL query.
## Papers
### When ground truth is unavailable - precision of aerial mappers without knowing the ground truth (literally!)
The following paper was my initial foray into this problem. It considers how to figure out the precision error that multiple maps of the ground are making. In hindsight, you could use the same algebraic set-up of the problem for figuring out the precision error of a collection of regressors. This work is notable in that it solves the problem even when the regressors are correlated using ideas from compressed sensing. It is a rare algorithm in the field of ground truth inference that can deal with correlated decision makers.
[Autonomous Geometric Precision Error Estimation in Low-Level Computer Vision Tasks](http://icml2008.cs.helsinki.fi/papers/121.pdf)
### When ground truth is private - accuracy of a statistical Unique ID system without knowing the identity of the users
This paper illustrates inferring a statistic of the ground truth when it is private - the true identity of users that arrive at a company that sells a unique ID service. This illustrates that it is possible to respect the privacy of users *and* measure the accuracy of your service.
[Algebra of Ground Truth Inference for Web Unique Identifiers](./papers/bc-id-ground-truth-wsdm-2015.pdf)