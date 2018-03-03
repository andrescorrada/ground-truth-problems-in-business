# Ground Truth Problems in Business
Collection of papers and presentations related to ground truth inference in data science
![Flammarion engraving](img/Flammarion.jpg)

The Flammarion engraving is frequently taken as a metaphor for piercing the veil of reality to understand what is really going on. The engraving also illustrates the goal of solving *ground truth problems* in business. In your company the ground truth of the production data stream may not be known. Or it could be hard to compute. Or private.

This collection contains examples of my work that solve the ground truth inference problem by estimating a statistic of ground truth without knowing ground truth itself.

The term *ground truth* sounds fancy and philosophical but it is not. It is easy to understand. It is just a generic term for the different forms it takes as detailed knowledge about your data. Let me mention a few.

### When you refuse to remember the ground truth

 The individual numbers in a long list of numbers would be a simple example of ground truth. If you have all the numbers on that list. you can calculate any statistic you want - its mean, its quartiles, etc. But suppose you just wanted to know the mean. Then you can get away with just keeping a running sum and a counter. You are able to calculate a statistic of the ground truth while refusing to remember all of it at once! People usually call these sort of computations - *data stream algorithms*. 

The [./hyperloglog](./hyperloglog/) folder contains work I have done with one such data stream algorithm, HyperLogLog, invented by Flajolet et al to count distincts in a database. I just applied the measurement over and over so I could measure time constants in a huge ad-tech database where ground truth for those time constants would have been impossibly expensive to compute.

### When ground truth is unknown or impossible to get

Here is another example of ground truth. Let's take a case I have solved - the accuracy of binary classifiers when label ground truth is not known. You have a bunch of data and each of your data points has an "A" or "B" label. The ground truth for that data would be the list of the true labels for each of the data points,
<a href="https://www.codecogs.com/eqnedit.php?latex=\{\ell_{i,\text{true}}\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\{\ell_{i,\text{true}}\}" title="\{\ell_{i,\text{true}}\}" /></a>.

And lastly, consider a company that sells speech recognition as a service to call centers. Ground truth could be the transcripts for all the audio it processed daily in production.

### The solution to all ground truth problems
The way to get around the problem of not having ground truth is to realize that, for most business decisions, the role of ground truth is to allow a statistic of ground truth to be computed! Ground truth is used to compute the statistic and then "discarded"! So if you can estimate the statistic directly, you eliminate the problem of not having the ground truth.

## Decisions not Details
Business decisions are frequently driven by average or SLA performance. Not all output is expected to be perfect and statistics of the data are used to specify SLA agreements. The most accurate algorithm is measured in the aggregate with decision makers not wanting to get into the details of the performance. I never attended a meeting during my days in speech recognition where Word Error Rate (WER) was not the only metric used to select best production algorithm after all other engineering constraints were satisfied.

The same observation applies to Marketing. Consider a marketing question, say, what percentage of our users visited our publisher network more than once last month? This statistic, the actual percentage,  is another example a computation where end users do not care about the details of the data.

So if the reason for ground truth is to compute the statistic, can I just compute the statistic and forget about the ground truth? Anybody familiar with data streaming algorithms understands this rationale.

## Precision is expensive, accuracy is not
Another theme that comes up in ground truth problems is the distinction between accuracy and precision error. You have experienced this if you have tweaked a zeroing screw on a mechanical weight scale or used the focus on your camera. Accuracy is cheap and easy. Precision, as in good quality lenses that perform uniformly over the whole view field, is expensive. So, while ground truth inference algorithms cannot frequently measure your accuracy error, they can measure your precision error. Hence they give you insight on the hardest quality measurement of your company's product - its precision.

## Decisions not Predictions
There is an important distinction to be made between using data science for decisions versus predictions. The business in "Ground Truth Problems in Business" comes from focusing on facilitating decisions in business, not predictions.

Why? Because many times you can solve business ground truth problems when you abandon prediction and focus on decision. And that distinction is reflected in a common "flaw" for some of the methods presented here. They are precise but sometimes not accurate.

Take again the case of binary classification. The reality for people that do not have the ground truth for the labels of a classifier's decisions looks like this - a solid rectangle of ignorance.

The binary classifier ground truth inference algorithm I have invented gives you this picture - two thin peaks. It is precise but not accurate.

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

## Technology
Data Engines Corporation (I am a founder) [owns patent 9,646249](http://patft.uspto.gov/netacgi/nph-Parser?Sect1=PTO2&Sect2=HITOFF&p=1&u=%2Fnetahtml%2FPTO%2Fsearch-bool.html&r=1&f=G&l=50&co1=AND&d=PTXT&s1=9,646,249.PN.&OS=PN/9,646,249&RS=PN/9,646,249) to a polynomial method for measuring the accuracy of binary classifiers when correct labels are unavailable. 

The basic idea behind the technology in the patent is explained in- [Independent Binary Classifiers](classification/IndependentBinaryClassifiers.nb) ,a Mathematica notebook showing the algebraic nature of the algorithm.
An interesting result here is that at least three classifiers are needed. The same limit (at least three) was encountered in the regression problem solved by the aerial mapping work discussed above.