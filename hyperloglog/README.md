# When ground truth is expensive - data stream algorithms
Here you will find work I have done with HyperLogLog, a well-known data stream algorithm. Streaming algorithms are usually not thought off in the context of ground truth inference. But I see some similarities. In this case, data stream algorithms are ground truth statistic computations that refuse to remember the ground truth. A nice side-effect of that forgetting of ground truth is that they become private. So the measurements I describe here that look at the dynamics of IPs in a huge ad-network over a two-week period could easily be used in GDPR countries that consider IPs private data.
![A First Arrivals in not A](./AvsNotAIPFirstArrivalMatchRate.png)
The figure above is a measurement I carried out to measure time constants for data flows between two parts of a company's ad-network. It would have been impossible to carry out this work using formally correct SQL queries of the company's database. Instead, I used HyperLogLog to take hourly sketches of the IP uniques in different data sources. The plot above was done in a series post-processing steps that computed union and intersection counts for all the sketches I had created. The rest of this README explains how I did it in more detail. Spoiler - not A is a better data source.
## Unions and Intersections with HyperLogLog
A nice property of the HyperLogLog unique sketch is that it is composable. You can compose two HLL sketches and get exactly the same result as if you had processed the stream as one instead of two parts. So composition gives you the union of the uniques in the two original streams. In fact, everything that I am going to talk about from now on only depends on that property of HyperLogLog (besides that it gives you a count estimate!). Any other algorithm for counting uniques that composed like HyperLogLog would work just as fine.
### Intersection count
Suppose you have two streams where you have sampled the uniques. This leads to HLL_A and HLL_B. We can use the HLL algorithm to count the sizes of A and B. What is the size of A intersection B?
size_intersection = size_a + size_b - size_union_a_b

## Dynamics of data flow in a database

Let's shift now the phenomena at hand - how does data flow in time in my company's network? One way to capture that is to ask what is the average time that you have to wait before you see something again that you just saw? I call that the time of first arrival.

With HyperLogLog we can ask this question en masse. We take as our source some unique sketch, say the sketch for the uniques observed in a given day. Now consider the unique sketches the following days. By using union and intersection operations, we can compute what percentage of uniques seen in the source hour have appearead in source B after x hours. That is what you are seeing in the plot above.

A sideways view of the plot may help clarify what you are seeing. Here I am plotting the match rate as a function of time.
