# A Call to Experimentation and Invention In Algebraic Evaluators of Noisy AI Judges

![Algebraic evaluation of four noisy UCI Adult classifiers](img/UCIAdultPanel.jpg)

Who judges the judges? The problem of the authority of noisy judges when we ourselves don't know their correct answers is pervasive in society and technology. In AI it is exemplified by the Stanford HAI AI Audit Challenge. Our submission to the challenge is this open source repository
highlighting the technology behind our GroundSeer(tm) product.

The submission focuses on one aspect of the AI Audit Challenge - the ubiquity of black-box
noisy AI algorithms. How can we know that these algorithms are working correctly ignorance
deployed? How can we have any assurance of their correctness without access to their internals
so we can audit them? We need to be able to monitor AI algorithms on the wild and we need
to do so robustly. GroundSeer(tm) points in one direction that can help us with this grand
challenge. Its 2010 patent is the world's first distribution-free evaluator of noisy AI
judges.

The safety engineer and the philosopher face the same "last mile verification" problem.
They must both evaluate noisy judges without the benefit of the ground truth. GroundSeer(tm)
is one way to mitigate this problem. It is one example of a class of algorithms that we
claim need much more research - algebraic evaluators of noisy AI judges. Our submission
is also a call to the curious inventors of the World to explore this "new" approach.

The resources in this repository should allow anyone in the World curious about algebra and
AI safety to explore this new approach. The core of that exploration is an initial app -
MappingYourAIAlarm.nb. All the code in this repository is written in Mathematica. This
platform for the Wolfram Language is perfect for our task. Mathematica neatly integrates
the data, programming and algebraic aspects of our new way for evaluating noisy AI judges.
Anybody with access to a RaspberryPi can execute and experiment with this code. We hope
they do.

## The role of distribution-free evaluators of noisy AI judges in AI safety and monitoring

### Robust to out-of-distribution shifts between training and deployment.
### Able to alarm on the failure of their own evaluation assumptions.
### Accessible to highly motivated high school students.
