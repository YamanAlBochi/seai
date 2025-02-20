---
author: Eunsuk Kang & Christian Kaestner
title: "17-645: Summary and Reflection"
semester: Fall 2022
footer: "17-645 Machine Learning in Production • Christian Kaestner, Carnegie Mellon University • Fall 2022"
license: Creative Commons Attribution 4.0 International (CC BY 4.0)
---  
<!-- .element: class="titleslide"  data-background="../_chapterimg/24_summary.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Summary & Reflection



---
# Today

<!-- colstart -->
(1)

**Looking back at the semester**

(413 slides in 40 min)

<!-- col -->
(2)

**Discussion of future of ML in Production**

<!-- col -->
(3)

**Feedback for future semesters**

<!-- colend -->



---
<!-- .element: class="titleslide"  data-background="../_chapterimg/01_intro.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Motivation, Syllabus, and Introductions



----
## Learning Goals

* Understand how ML components are parts of larger systems
* Illustrate the challenges in engineering an ML-enabled system beyond accuracy
* Explain the role of specifications and their lack in machine learning and the relationship to deductive and inductive reasoning
* Summarize the respective goals and challenges of software engineers vs data scientists
* Explain the concept and relevance of "T-shaped people"

----
## Catastrophic Success

![Crowd](crowd.jpg)

----

![competitor](transcription.png)

----

## Breakout: Likely challenges in building commercial product?

<div class="smallish">

As a group, think about challenges that the team will likely focus when turning their research into *a product*:
* One machine-learning challenge
* One engineering challenge in building the product
* One challenge from operating and updating the product
* One team or management challenge
* One business challenge
* One safety or ethics challenge

*Post answer to `#lecture` on Slack and tag all group members*

</div>

----
## ML in a Production System


![Architecture diagram of transcription service; many components, not just ML](transcriptionarchitecture2.svg)
<!-- .element: class="plain stretch" -->

----

<svg version="1.1" viewBox="0.0 0.0 800 400" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns="http://www.w3.org/2000/svg" class="stretch">
        <style>
    text { font: 60px sans-serif; }
        </style>
        <circle r="180" cx="250", cy="200" fill="#b9ff00" fill-opacity="0.514" />
        <circle r="180" cx="550", cy="200" fill="#ff5500" fill-opacity="0.514" />
        <text x=230 y=160 dominant-baseline="middle" text-anchor="middle">Data</text>
        <text x=230 y=240 dominant-baseline="middle" text-anchor="middle">Scientists</text>
        <text x=570 y=160 dominant-baseline="middle" text-anchor="middle">Software</text>
        <text x=570 y=240 dominant-baseline="middle" text-anchor="middle">Engineers</text>
</svg>


<div class="small">and Data engineers + Domain specialists + Operators + Business team + Project managers + Designers, UI Experts + Safety, security specialists + Lawyers + Social scientists + ...</div>


----

![Unicorns](roles_venn.svg)<!-- .element: class="plain" style="width:46%"-->


By Steven Geringer, via Ryan Orban. [Bridging the Gap Between Data Science & Engineer: Building High-Performance Teams](https://www.slideshare.net/ryanorban/bridging-the-gap-between-data-science-engineer-building-highperformance-teams/3-Software_Engineer_Data_Engineer_Data). 2016
<!-- .element: class="smaller"-->


----
## T-Shaped People

*Broad-range generalist + Deep expertise*

![T-Shaped](tshaped.png)
<!-- .element: class="plain" -->


<!-- reference -->
Figure: Jason Yip. [Why T-shaped people?](https://medium.com/@jchyip/why-t-shaped-people-e8706198e437). 2018


----
# Syllabus and Class Structure

17-445/17-645/17-745, Fall 2022, 12 units

Monday/Wednesdays 1:25-2:45pm

Recitation Fridays 10:10-11:00am / 1:25-2:45pm

----
## First Homework Assignment

<!-- colstart -->
*"Coding warmup assignment"*

[Out now](https://github.com/ckaestne/seai/blob/F2022/assignments/I1_mlproduct.md), due Sep 7

Enhance simple web *application* with ML-based feature: Automated image captioning

Open ended coding assignment, change existing code, learn new APIs


<!-- col -->
![Screenshot of Albumy](albumy.png)
<!-- colend -->


----

![Class Overview](overview.svg)
<!-- .element: class="plain" -->


----
## Reading Assignments & Quizzes

<!-- colstart -->
*Building Intelligent Systems*
by Geoff Hulten

https://www.buildingintelligentsystems.com/

Most chapters assigned at some point in the semester

Supplemented with research articles, blog posts, videos, podcasts, ...

[Electronic version](https://cmu.primo.exlibrisgroup.com/permalink/01CMU_INST/6lpsnm/alma991019649190004436) in the library

<!-- col -->

![Building intelligent systems book](book.webp)

<!-- colend -->


----
## Timeline


![Timeline](timeline.svg)<!-- .element: class="plain" style="width:100%" -->


----
## Grading Philosophy

Specification grading, based in adult learning theory

Giving you choices in what to work on or how to prioritize your work

We are making every effort to be clear about expectations (specifications), will clarify if you have questions


Assignments broken down into expectations with point values, each graded **pass/fail**

Opportunities to resubmit work until last day of class

[[Example]](https://github.com/ckaestne/seai/blob/F2022/assignments/I1_mlproduct.md#grading)



----
## ML Models Make Mistakes

![ML image captioning mistakes](mistakes.jpg)
<!-- .element: class="r-stretch" -->


Note: Source: https://www.aiweirdness.com/do-neural-nets-dream-of-electric-18-03-02/

----
## Lack of Specifications

```java
/**
  Return the text spoken within the audio file
  ????
*/
String transcribe(File audioFile);
```

----
## It's not all new

We routinely build:
* Safe software with unreliable components
* Cyberphysical systems
* Non-ML big data systems, cloud systems
* "Good enough" and "fit for purpose" not "correct"

ML intensifies our challenges

----
## Complexity
![Complexity prediction](complexity.svg)
<!-- .element: class="plain" -->

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/02_systems.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# From Models to Systems

<!-- Image: https://www.pexels.com/photo/delivery-robot-on-pavement-under-trees-8566570/ -->


----
# Learning goals

* Explain how machine learning fits into the larger picture of building and maintaining production systems
* Explain the consequences of the shift from deductive to inductive reasoning for abstraction and composition
* Explain the modularity implications of having machine-learning components without specifications
* Describe the typical components relating to AI in an AI-enabled system and typical design decisions to be made






----
## Why do we care about image captioning?

![Image captioning one step](imgcaptioning.png)



----
![Image Search on Google Photos](imagesearch.png)
<!-- .element: class="plain stretch" -->


----
## Products using Image Synthesis?

![Dall-e generated example of chairs in the form of an avocado](dall-e.png)
<!-- .element: class="plain stretch" -->

<!-- references_ -->
From https://openai.com/blog/dall-e/


----
## Traditional Model Focus (Data Science)

![](pipeline.svg)
<!-- .element: class="plain" -->

Focus: building models from given data, evaluating accuracy


----
## Automating Pipelines and MLOps (ML Engineering)

![](pipeline2.svg)
<!-- .element: class="plain" -->

Focus: experimenting, deploying, scaling training and serving, model monitoring and updating

----
## ML-Enabled Systems (ML in Production)

![](pipeline-in-system.svg)<!-- .element: class="plain" style="width:90%" -->

Interaction of ML and non-ML components, system requirements, user interactions, safety, collaboration, delivering products



----
# Model vs System Goals

<!-- twitter https://twitter.com/Fra_Pochetti/status/1502708228173578240?t=dNbEpulbras763WHt-QZvg&s=03 -->

----
## Case Study: Self-help legal chatbot

![Website](lawchat.png)
<!-- .element: class="stretch" -->


<!-- references_ -->

Based on the excellent paper: Passi, S., & Sengers, P. (2020). [Making data science systems work](https://journals.sagepub.com/doi/full/10.1177/2053951720939605). Big Data & Society, 7(2).

Note: Screenshots for illustration purposes, not the actual system studied




----
## Machine learning that matters

<div class="smallish">

* 2012(!) essay lamenting focus on algorithmic improvements and benchmarks
  - focus on standard benchmark sets, not engaging with problem: Iris classification, digit recognition, ...
  - focus on abstract metrics, not measuring real-world impact: accuracy, ROC
  - distant from real-world concerns
  - lack of follow-through, no deployment, no impact
* Failure to *reproduce* and *productionize* paper contributions common
* Ignoring design choices in how to collect data, what problem to solve, how to design human-AI interface, measuring impact, ...
* *Argues: Should focus on making impact -- requires building systems*

</div>

<!-- references -->

Wagstaff, Kiri. "Machine learning that matters." In Proceedings of the 29 th International Conference on Machine Learning, (2012).









----
# Systems Thinking

![](system.svg)
<!-- .element: class="plain" -->


----
## Feedback Loops


![Feedback loop with data creating model, creating decisions, creating data](feedbackloop.svg)
<!-- .element: class="plain stretch" -->


----
## Safety is a System Property

* Code/models are not unsafe, cannot harm people
* Systems can interact with the environment in ways that are unsafe

![Smart Toaster](toaster.jpg)

----
## Safety Assurance in/outside the Model

<!-- colstart -->
<div class="smallish">

In the model
  - Ensure maximum toasting time
  - Use heat sensor and past outputs for prediction
  - Hard to make guarantees

Outside the model (e.g., "guardrails")
  - Simple code check for max toasting time
  - Non-ML rule to shut down if too hot
  - Hardware solution: thermal fuse

</div>

<!-- col -->

![Thermal fuse](thermalfuse.png)
(Image CC BY-SA 4.0, C J Cowie)
<!-- .element: class="small" -->
<!-- colend -->

----
## Presenting Intelligence

**Automate**: Take action on user's behalf

**Prompt**: Ask the user if an action should be taken

**Organize/Annotate/Augment**: Add information to a display

Hybrids of these





----
## Breakout Discussion: Experience Design

<div class="small">

<!-- colstart -->

Fall detection for elderly people:

![Smart watch](smartwatch.jpg)<!-- .element: style="width:70%" -->



<!-- col -->

Safe browsing: Blocking malicious web pages

![Safe browsing warning](warning.png)

<!-- colend -->

Discuss in group and post to `#lecture` tagging all members: 
(1) How do we present the intelligence to the user?
(2) Justify in terms of system goals, forcefulness, frequency, value of correct and cost of wrong predictions

</div>

Notes:
Devices for older adults to detect falls and alert caretaker or emergency responders automatically or after interaction. Uses various inputs to detect falls.
Read more: [How fall detection is moving beyond the pendant](https://www.mobihealthnews.com/content/how-fall-detection-moving-beyond-pendant), MobiHealthNews, 2019


----
## Things change...


<!-- colstart -->


Newer better models released (better model architectures, more training data, ...)

Goals and scope change (more domains, handling dialects, ...)

The world changes (new products, names, slang, ...)

Online experimentation



<!-- col -->

![Architecture diagram of transcription service; many components, not just ML](transcriptionarchitecture.svg)
<!-- .element: class="plain" -->


<!-- colend -->


----
## Monitoring in Production

Design for telemetry

<!-- colstart -->
![Safe Browsing Feedback](safe-browsing-feedback.png)
<!-- col -->
![Safe Browsing Statistics](safe-browsing-stats.png)
<!-- colend -->


----
## Pipelines Thinking is Challenging

<div class="smallish">

In enterprise ML teams:
* Data scientists often focus on modeling in local environment, model-centric workflow
* Rarely robust infrastructure, often monolithic and tangled
* Challenges in deploying systems and integration with monitoring, streams etc

Shifting to pipeline-centric workflow challenging
* Requires writing robust programs, slower, less exploratory
* Standardized, modular infrastructure 
* Big conceptual leap, major hurdle to adoption

</div>

<!-- references -->

O'Leary, Katie, and Makoto Uchida. "[Common problems with Creating Machine Learning Pipelines from Existing Code](https://research.google/pubs/pub48984.pdf)." Proc. Third Conference on Machine Learning and Systems (MLSys) (2020).



---
<!-- .element: class="titleslide"  data-background="../_chapterimg/03a_teamwork.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Teamwork - A Primer


<!-- image: https://pixabay.com/photos/team-grass-cheer-field-game-sport-2444978/ -->



----
## Who has had bad experiences in teams? Student teams? Teams in industry?

![Frustration](frustrated.jpeg)<!-- .element: class="plain" style="width:70%" -->

----
## Summary: How would you handle...

<div class="small">

1. One team member has very little technical experience and is struggling with basic Python scripts and the Unix shell. It is faster for other team members to take over the task rather than helping them.
2. You divide the work and but when you try to integrate on the evening before the deadline you learn that one team member has failed to complete their part. They tried the day before, but got stuck with a compatibility problem.
3. After last minute stress at the last assignment, you team agrees to start earlier and to integrate at a milestone days before the deadline to leave a buffer. Yet you see little progress from half the team in GitHub and hardly anybody responds in Slack. Little is done at the agreed milestone. The work gets done before the deadline, but with the same stress as in the last assignment.
4. This homework is low priority for one team member. They rarely contribute beyond the bare minimum at the last minute. (The rest of the team grudgingly compensates and achieves full points for the assignment. You do not feel comfortable criticizing the student as it may negatively affect their grade.)

</div>

----
## Teamwork Policies and Support in this Course

* Teams can set their own priorities and policies -- do what works for you, experiment
    * Not everybody will contribute equally to every assignment -- that's okay
    * Team members have different strength and weaknesses -- that's good
* We will intervene in *team citizenship* issues!

> Golden rule: Try to do what you agreed to do by the time you agreed to. If you cannot, seek help and communicate clearly and early.


---
<!-- .element: class="titleslide"  data-background="../_chapterimg/03_accuracy.jpg" -->
<div class="stretch"></div>


## Machine Learning in Production


# Model Correctness and Accuracy

<!-- Image source: https://pixabay.com/photos/darts-dartboard-game-sports-target-102919/ -->


----
# Learning Goals

* Select a suitable metric to evaluate prediction accuracy of a model and to compare multiple models
* Select a suitable baseline when evaluating model accuracy
* Know and avoid common pitfalls in evaluating model accuracy
* Explain how software testing differs from measuring prediction accuracy of a model

----
# Model Quality


**First Part:** Measuring Prediction Accuracy
* the data scientist's perspective

**Second Part:** What is Correctness Anyway?
* the role and lack of specifications, validation vs verification

**Third Part:** Learning from Software Testing 
* unit testing, test case curation, invariants, simulation (next lecture)

**Later:** Testing in Production
* monitoring, A/B testing, canary releases (in 2 weeks)





----
## Confusion/Error Matrix

<div class="small">

<!-- colstart -->

| | **Actually Grade 5 Cancer** | **Actually Grade 3 Cancer** | **Actually Benign** |
| :--- | --- | --- | --- |
|**Model predicts Grade 5 Cancer** | **10** | 6 | 2 |
|**Model predicts Grade 3 Cancer** | 3 | **24**  | 10 |
|**Model predicts Benign** | 5 | 22 | **82** |


<!-- col -->


$\textit{accuracy} = \frac{\textit{correct predictions}}{\textit{all predictions}}$

Example's accuracy 
        = $\frac{10+24+82}{10+6+2+3+24+10+5+22+82} = .707$

```scala
def accuracy(model, xs, ys):
  count = length(xs)
  countCorrect = 0
  for i in 1..count:
    predicted = model(xs[i])
    if predicted == ys[i]:
      countCorrect += 1
  return countCorrect / count
```

<!-- colend -->

</div>


----

[![Recall/Precision visualization](recallprecision.png)](https://en.wikipedia.org/wiki/Precision_and_recall#/media/File:Precisionrecall.svg)
<!-- .element: class="stretch" -->

<!-- references_ -->

(CC BY-SA 4.0 by [Walber](https://en.wikipedia.org/wiki/Precision_and_recall#/media/File:Precisionrecall.svg))

----
## Area Under the Curve

Turning numeric prediction into classification with threshold ("operating point")

![Recall/Precision Plot](prcurve.png)
<!-- .element: class="stretch" -->

Notes: The plot shows the recall precision/tradeoff at different thresholds (the thresholds are not shown explicitly). Curves closer to the top-right corner are better considering all possible thresholds. Typically, the area under the curve is measured to have a single number for comparison.


----

## The Legend of the Failed Tank Detector

<!-- colstart -->
![Tank in Forest](tank.jpg)
<!-- col -->
![Forest](forest.jpg)
<!-- colend -->

Notes:
Widely shared story, authenticity not clear:
AI research team tried to train image recognition to identify tanks hidden in forests, trained on images of tanks in forests and images of same or similar forests without tanks. The model could clearly separate the learned pictures, but would perform poorly on other pictures.

Turns out the pictures with tanks were taken on a sunny day whereas the other pictures were taken on a cloudy day. The model picked up on the brightness of the picture rather than the presence of a tank, which worked great for the training set, but did not generalize.

Pictures: https://pixabay.com/photos/lost-places-panzer-wreck-metal-3907364/, https://pixabay.com/photos/forest-dark-woods-trail-path-1031022/




----
## Production Data -- The Ultimate Unseen Validation Data

more in a later lecture


<div class="tweet" data-src="https://twitter.com/changelog/status/1137359428632621060"></div>


----
## Common Pitfalls of Evaluating Model Quality?

<!-- discussion -->


----
## Test Data not Representative

Often neither training nor test data representative of production data 

![MNIST Fashion Dataset Examples](MNIST-fashion.png)
<!-- .element: class="stretch" -->



----
## Shortcut Learning

![Shortcut learning illustration from paper below](shortcutlearning.png)
<!-- .element: class="plain stretch" -->

<!-- references_ -->
Figure from: Geirhos, Robert, et al. "[Shortcut learning in deep neural networks](https://arxiv.org/abs/2004.07780)." Nature Machine Intelligence 2, no. 11 (2020): 665-673.

Note: (From figure caption) Toy example of shortcut learning in neural networks. When trained on a simple dataset
of stars and moons (top row), a standard neural network (three layers, fully connected) can easily
categorise novel similar exemplars (mathematically termed i.i.d. test set, defined later in Section 3).
However, testing it on a slightly different dataset (o.o.d. test set, bottom row) reveals a shortcut
strategy: The network has learned to associate object location with a category. During training,
stars were always shown in the top right or bottom left of an image; moons in the top left or bottom
right. This pattern is still present in samples from the i.i.d. test set (middle row) but not in o.o.d. test
images (bottom row), exposing the shortcut.

----
## Data Leakage during Data Preprocessing

```python
wordsVectorizer = CountVectorizer().fit(text)
wordsVector = wordsVectorizer.transform(text)
invTransformer = TfidfTransformer().fit(wordsVector)
invFreqOfWords = invTransformer.transform(wordsVector)
X = pd.DataFrame(invFreqOfWords.toarray())

train, test, spamLabelTrain, spamLabelTest = 
                   train_test_split(X, y, test_size = 0.5)
predictAndReport(train = train, test = test)
```



----
## Independence of Data: Temporal

![Temporal dependence](temporaldependence.svg)
<!-- .element: class="stretch plain" -->

Note: The curve is the real trend, red points are training data, green points are validation data. If validation data is randomly selected, it is much easier to predict, because the trends around it are known.


----
## Independence of Data: Related Datapoints

Example: Kaggle competition on detecting distracted drivers

![Driver Picture 1](driver_phone.png) ![Driver Picture 2](driver_phone2.png)
<!-- .element: class="stretch" -->

Relation of datapoints may not be in the data (e.g., driver)

<!-- references_ -->

https://www.fast.ai/2017/11/13/validation-sets/

Note: 
Many potential subtle and less subtle problems:
* Sales from same user
* Pictures taken on same day




----
# Part 2:
# What is Correctness Anyway?

specifications, bugs, fit


----
## SE World: Evaluating a Component's Functional Correctness

<div class="smallish">


*Given a specification, do outputs match inputs?*

```java
/**
 * compute deductions based on provided adjusted 
 * gross income and expenses in customer data.
 *
 * see tax code 26 U.S. Code A.1.B, PART VI
 */
float computeDeductions(float agi, Expenses expenses);
```

**Each mismatch is considered a bug, should to be fixed.†**

</div>

<div class="smaller">
(†=not every bug is economical to fix, may accept some known bugs)
</div>


----
## Validation vs Verification

![Validation vs Verification](validation.png)
<!-- .element: class="plain" -->


----
## No specification!

<div class="smallish">

![Cancer prognosis with ML](cancerpred.png)

Use ML precisely because no specifications (too complex, rules unknown)
* No specification that could tell us for any input whether the output is correct
* Intuitions, ideas, goals, examples, "implicit specifications", but nothing we can write down as rules!
* *We are usually okay with some wrong predictions*

</div>

----
## Testing a Machine Learning Model?


```java
// detects cancer in an image
boolean hasCancer(Image scan);

@Test
void testPatient1() {
  assertEquals(loadImage("patient1.jpg"), false);
}
@Test
void testPatient2() {
  assertEquals(loadImage("patient2.jpg"), false);
}
```



----
## All Models Are Wrong


> All models are approximations. Assumptions, whether implied or clearly stated, are never exactly true. **All models are wrong, but some models are useful**. So the question you need to ask is not "Is the model true?" (it never is) but "Is the model good enough for this particular application?" -- George Box


<!-- references -->
See also https://en.wikipedia.org/wiki/All_models_are_wrong
<br/>&nbsp;


----
## Deductive vs Inductive Reasoning



[![Contrasting inductive and deductive reasoning](inductive.png)](https://danielmiessler.com/blog/the-difference-between-deductive-and-inductive-reasoning/)
<!-- .element: class="stretch" -->

<!-- references_ -->

(Daniel Miessler, CC SA 2.0)




----
## Machine Learning Models Fit, or Not

* A model is learned from given data in given procedure 
    - The learning process is typically not a correctness concern
    - The model itself is generated, typically no implementation issues
* Is the data representative? Sufficient? High quality?
* Does the model "learn" meaningful concepts?
*
* **Is the model useful for a problem?** Does it *fit*?
* Do model predictions *usually* fit the users' expectations?
* Is the model *consistent* with other requirements? (e.g., fairness, robustness)




























---
<!-- .element: class="titleslide"  data-background="../_chapterimg/03_modeltesting.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Model Testing beyond Accuracy

<p class="small" style="margin-top:0 !important">(Slicing, Capabilities, Invariants, Simulation, ...)</p>

<!-- image: https://pixabay.com/photos/microscope-slide-research-close-up-275984/ -->


----
# Learning Goals

* Curate validation datasets for assessing model quality, covering subpopulations and capabilities as needed
* Explain the oracle problem and how it challenges testing of software and models
* Use invariants to check partial model properties with automated testing
* Select and deploy automated infrastructure to evaluate and monitor model quality


----
# Curating Validation Data & Input Slicing

![Fruit slices](slices.jpg)


----
## Software Test Case Design

<div class="smallish">

**Opportunistic/exploratory testing:** Add some unit tests, without much planning

**Specification-based testing** ("black box"): Derive test cases from specifications
  - Boundary value analysis
  - Equivalence classes
  - Combinatorial testing
  - Random testing

**Structural testing** ("white box"): Derive test cases to cover implementation paths
  - Line coverage, branch coverage
  - Control-flow, data-flow testing, MCDC, ...

Test execution usually automated, but can be manual too; automated generation from specifications or code possible

</div>


----
## Not All Inputs are Equal

![Google Home](googlehome.jpg)
<!-- .element: class="stretch" -->

"Call mom"
"What's the weather tomorrow?"
"Add asafetida to my shopping list"


----
## Input Partitioning Example

<div class="small">

<!-- colstart -->
![Input partitioning example](inputpartitioning2.png)

Input divided by movie age. Notice low accuracy, but also low support (i.e., little validation data), for old movies.
<!-- col -->
![Input partitioning example](inputpartitioning.png)

Input divided by genre, rating, and length. Accuracy differs, but also amount of test data used ("support") differs, highlighting low confidence areas.
<!-- colend -->


</div>

<!-- references -->

Source: Barash, Guy, et al. "Bridging the gap between ML solutions and their business requirements using feature interactions." In Proc. FSE, 2019.


----
## Example: Model Impr. at Apple (Overton)

![Overton system](overton.png)
<!-- .element: class="stretch" -->


<!-- references_ -->

Ré, Christopher, Feng Niu, Pallavi Gudipati, and Charles Srisuwananukorn. "[Overton: A Data System for Monitoring and Improving Machine-Learned Products](https://arxiv.org/abs/1909.05372)." arXiv preprint arXiv:1909.05372 (2019).




----
# Testing Model Capabilities


![Checklist](checklist.jpg)
<!-- .element: class="stretch" -->


<!-- references_ -->

Further reading: Christian Kaestner. [Rediscovering Unit Testing: Testing Capabilities of ML Models](https://towardsdatascience.com/rediscovering-unit-testing-testing-capabilities-of-ml-models-b008c778ca81). Toward Data Science, 2021.

<!-- figure: https://pixabay.com/photos/checklist-goals-box-notebook-pen-2589418/ -->

----
## Testing Capabilities

![Examples of Capabilities from Checklist Paper](capabilities1.png)


<!-- references -->

From: Ribeiro, Marco Tulio, Tongshuang Wu, Carlos Guestrin, and Sameer Singh. "[Beyond Accuracy: Behavioral Testing of NLP Models with CheckList](https://homes.cs.washington.edu/~wtshuang/static/papers/2020-acl-checklist.pdf)." In Proceedings ACL, p. 4902–4912. (2020).



----
## Generating Test Data for Capabilities

**Idea 1: Domain-specific generators**

Testing *negation* in sentiment analysis with template: <br/>
`I {NEGATION} {POS_VERB} the {THING}.`

Testing texture vs shape priority with artificial generated images:
![Texture vs shape example](texturevsshape.png)


<!-- references -->
Figure from Geirhos, Robert, Patricia Rubisch, Claudio Michaelis, Matthias Bethge, Felix A. Wichmann, and Wieland Brendel. “ImageNet-trained CNNs are biased towards texture; increasing shape bias improves accuracy and robustness.” In Proc. International Conference on Learning Representations (ICLR), (2019).


----
## Generating Test Data for Capabilities

**Idea 3: Crowd-sourcing test creation**

Testing *sarcasm* in sentiment analysis: Ask humans to minimally change text to flip sentiment with sarcasm

Testing *background* in object detection: Ask humans to take pictures of specific objects with unusual backgrounds

![Example of modifications to text](sarcasm.png)

<!-- references -->

Figure from: Kaushik, Divyansh, Eduard Hovy, and Zachary C. Lipton. “Learning the difference that makes a difference with counterfactually-augmented data.” In Proc. International Conference on Learning Representations (ICLR), (2020).





----
# Automated (Random) Testing and Invariants

(if it wasn't for that darn oracle problem)

![Random dice throw](random.jpg)

<!-- https://pixabay.com/photos/dice-game-random-gambling-1963036/ -->

----
## Cancer in Random Image?

![](white-noise.jpg)

----
## The Oracle Problem

*How do we know the expected output of a test?*

```java
assertEquals(??, factorPrime(15485863));
```

<!-- discussion -->



----
## Examples of Invariants

<div class="smallish">


* Credit rating should not depend on gender:
    - $\forall x. f(x[\text{gender} \leftarrow \text{male}]) = f(x[\text{gender} \leftarrow \text{female}])$
* Synonyms should not change the sentiment of text:
    - $\forall x. f(x) = f(\texttt{replace}(x, \text{"is not", "isn't"}))$
* Negation should swap meaning:
    - $\forall x \in \text{"X is Y"}. f(x) = 1-f(\texttt{replace}(x, \text{" is ", " is not "}))$
* Robustness around training data:
    - $\forall x \in \text{training data}. \forall y \in \text{mutate}(x, \delta). f(x) = f(y)$
* Low credit scores should never get a loan (sufficient conditions for classification, "anchors"):
    - $\forall x. x.\text{score} < 649 \Rightarrow \neg f(x)$

Identifying invariants requires domain knowledge of the problem!

</div>


----
# Simulation-Based Testing

![Driving a simulator](simulationdriving.jpg)
<!-- .element: class="stretch" -->



----
## One More Thing: Simulation-Based Testing

<div class="small">

<!-- colstart -->

* Derive input-output pairs from simulation, esp. in vision systems
* Example: Vision for self-driving cars:
    * Render scene -> add noise -> recognize -> compare recognized result with simulator state
* Quality depends on quality of simulator: 
    * examples: render picture/video, synthesize speech, ... 
    * Less suitable where input-output relationship unknown, e.g., cancer prognosis, housing price prediction
<!-- col -->
![Simulation is the inverse of prediction](simulationbased-testing.svg)
<!-- .element: class="plain" -->

<!-- colend -->

</div>

<!-- references -->

Further readings: Zhang, Mengshi, Yuqun Zhang, Lingming Zhang, Cong Liu, and Sarfraz Khurshid. "DeepRoad: GAN-based metamorphic testing and input validation framework for autonomous driving systems." In Proc. ASE. 2018.


----

## Test Coverage

![](coverage.png)


----
# Continuous Integration for Model Quality

[![Uber's internal dashboard](uber-dashboard.png)](https://eng.uber.com/michelangelo/)
<!-- .element: class="stretch" -->


----
## Project Milestone 1: Modeling and First Deployment


---
<!-- .element: class="titleslide"  data-background="../_chapterimg/05_measurement.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Goals and Measurement



----
## Exploring Requirements...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->


----


## Learning goals

* Judge when to apply ML for a problem in a system
* Define system goals and map them to goals for ML components
* Understand the key concepts and risks of measurement



----
## Today's Case Study: Spotify Personalized Playlists

[![Spotify Screenshot of (My) Personalized Playlists](spotify.png)](spotify.png)
<!-- .element: class="stretch" -->





----
## When to use Machine Learning

**Big problems:** Many inputs, massive scale

**Open-ended problems:** No single "final" solution; incremental
  improvements and growth over time

**Time-changing problems:** Adapting to constant changes, learning with users

**Intrinsically hard problems:** Unclear rules, heuristics perform poorly

**Examples?**

<!-- references -->
see Hulten, Chapter 2





----
## AI as Prediction Machines

<!-- colstart --> 

<div class="smallish">

AI: Higher accuracy predictions at much lower cost 

May use new, cheaper predictions for traditional tasks (**examples?**) 

May now use predictions for new kinds of problems (**examples?**) 

May now use more predictions than before  

(Analogies: Reduced cost of light; internet reduced cost of search) 

</div>

<!-- col --> 

![Book: Prediction Machines](predictionmachinescover.png) 
<!-- .element: class="stretch" --> 

<!-- colend --> 

Notes: May use new, cheaper predictions for traditional tasks -> inventory and demand forecast; May now use predictions for new kinds of problems -> navigation and translation 


----
## Layers of Success Measures

<!-- colstart -->

<div class="small">

* **Organizational objectives:** Innate/overall goals of the organization
* **Leading indicators:** Measures correlating with future success, from the business perspective
* **System goals:** Goals of the software system/feature to be built
* **User outcomes:** How well the system is serving its users, from the user's perspective
* **Model properties:** Quality of the model used in a system, from the model's perspective
 

*Ideally, these goals should be aligned with each other*

</div>

<!-- col -->

![Goal relationships](goal-relationships.svg)
<!-- .element: class="plain" -->

<!-- colend -->

----
## Breakout: Automating Admission Decisions

What are different types of goals behind automating admissions decisions to a Master's program?

As a group post answer to `#lecture` tagging all group members using template:
> Organizational goals: ...<br />
> Leading indicators: ...<br />
> System goals: ...<br />
> User goals: ...<br />
> Model goals: ...<br />



----
## Everything is Measurable

<div class="smallish">

1. If X is something we care about, then X, by definition, must be
detectable.
    * How could we care about things like “quality,” “risk,” “security,” or “public image” if these things were totally undetectable, directly or indirectly?
    * If we have reason to care about some unknown quantity, it is because we think it corresponds to desirable or undesirable results in some way.
2. If X is detectable, then it must be detectable in some amount.
	* If you can observe a thing at all, you can observe more of it or less of it
3. If we can observe it in some amount, then it must be measurable.


*But: Not every measure is precise, not every measure is cost effective*

</div>

<!-- references -->

Douglas Hubbard, “[How to Measure Anything: finding the value of intangibles in business](https://cmu.primo.exlibrisgroup.com/permalink/01CMU_INST/1feg4j8/alma991019515498904436)" 2014


----
## Composing/Decomposing Measures
Often higher-level measures are composed from lower level measures

Clear trace from specific low-level measurements to high-level metric

![Decomposition of a maintainability metric](maintainability-decomp.svg)
<!-- .element: class="plain" -->

<!-- references -->
For design strategy, see [Goal-Question-Metric approach](https://en.wikipedia.org/wiki/GQM)

----
## Stating Measures Precisely

<div class="smallish">

* Always be precise about metrics
    - "measure accuracy" -> "evaluate accuracy with MAPE"
    - "evaluate test quality" -> "measure branch coverage with Jacoco"
    - "measure execution time" -> "average and 90%-quantile response time for REST-API x under normal load"
    - "assess developer skills" -> "measure average lines of code produced per day and number of bugs reported on code produced by that developer"
    - "measure customer happiness" -> "report response rate and average customer rating on survey shown to 2% of all customers (randomly selected)"
* Ideally: An independent party should be able to independently set up infrastructure to measure outcomes

</div>


----
## Measuring

Three ingredients:
1. **Measure:** What do we try to capture?
2. **Data collection:** What data is collected and how?
3. **Operationalization:** How is the measure computed from the data?


----

## Streetlight effect

<!-- colstart -->

* A type of _observational bias_
* People tend to look for something where it’s easiest to do so
  * Use cheap proxy metrics that only poorly correlate with goal
  * e.g., number of daily active users as a measure of projected revenue

<!-- col -->

![Streetlight](streetlight.jpg)
<!-- .element: class="stretch" -->

<!-- colend -->

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/06_requirements.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Gathering Requirements



----
## Learning Goals

* Understand the role of requirements in ML-based systems and their
failures
* Understand the distinction between the world and the machine
* Understand the importance of environmental assumptions in
  establishing system requirements


----
## Facial Recognition in ATM

![ATM](atm.gif)
<!-- .element: class="stretch" -->

**Q. What went wrong? What is the root cause of the failure?**

----
## Automated Hiring

![Amazon Hiring Tool Scraped due to Bias](amazonhiring.png)
<!-- .element: class="stretch" -->

**Q. What went wrong? What is the root cause of the failure?**


----
## Machine vs World

![machine-world](worldvsmachine.svg)
<!-- .element: class="stretch plain" -->

----
## Shared Phenomena

![phenomena](phenomena.jpg)
<!-- .element: class="stretch" -->

<div class="smallish">

* Shared phenomena: Interface between the environment & software
  * Input: Lidar, camera, pressure sensors, GPS
  * Output: Signals generated & sent to the engine or brake control
* Software can influence the environment **only** through the shared interface
  * Unshared parts of the environment are beyond software’s control
  * We can only **assume** how these parts will behave

</div>

----
## Breakout: Lane Assist Assumptions

![lane-keeping](lane-keeping.png)
<!-- .element: class="stretch" -->

REQ: The vehicle must be prevented from veering off the lane.

SPEC: Lane detector accurately identifies lane markings in the input image; 
  the controller generates correct steering commands

**Discuss with your neighbor to come up with 2-3 assumptions**

----
## Lufthansa 2904 Runaway Crash


![Illustration of time elapsed between touchdown of the first main strut, the second and engagement of brakes.](lh2904_animation.gif)

<!-- references_ -->

CC BY-SA 3.0 [Anynobody](https://en.wikipedia.org/wiki/Lufthansa_Flight_2904#/media/File:Lufthansa_Flight_2904.gif)

----
## Breakout Session: Fall detection

![smart-watch](smartwatch.jpg)
<!-- .element: class="stretch" -->

As a group, post answer to `#lecture` and tag group members:
> Requirement: ...<br />
> Assumptions: ...<br />
> Specification: ...<br />
> What can go wrong: ... <br />


----
## What went wrong? (REQ, ASM, SPEC)?

![ATM](atm.gif)
<!-- .element: class="stretch" -->

----
## Understanding requirements is hard

* Customers don't know what they want until they see it
* Customers change their mind ("no, not like that")
* Descriptions are vague
* It is easy to ignore important requirements (privacy, fairness)
* Focused too narrowly on needs of few users
* Engineers think they already know the requirements
* Engineers are overly influenced by technical capability
* Engineers prefer elegant abstractions

**Examples?**

<!-- references -->

See also 🗎 Jackson, Michael. "[The world and the machine](https://web.archive.org/web/20170519054102id_/http://mcs.open.ac.uk:80/mj665/icse17kn.pdf)." In Proceedings of the International Conference on Software Engineering. IEEE, 1995.


----
## Requirements elicitation techniques

![Interview](interview.jpg)
<!-- .element: class="stretch" -->

<!-- source: https://www.pexels.com/photo/spiral-notebook-and-voice-recorder-on-sofa-chair-9400300/ -->

----
## ML Prototyping: Wizard of Oz

![Wizard of oz excerpt](wizard.gif)<!-- .element: style="width:800px" -->

Note: In a wizard of oz experiment a human fills in for the ML model that is to be developed. For example a human might write the replies in the chatbot. 

----
## Personas in GenderMag


![Gendermag](gendermag1.png)


See examples and details http://gendermag.org/foundations.php


----
## How much requirements eng. and when?

![Waterfall process picture](waterfall.svg)<!-- .element: class="plain" style="width:1100px" -->


----
# Homework I2: Requirements

Dashcam system


---
<!-- .element: class="titleslide"  data-background="../_chapterimg/07_mistakes.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Planning for Mistakes


----
## Learning goals:

* Consider ML models as unreliable components
* Use safety engineering techniques FTA, FMEA, and HAZOP to anticipate and analyze possible mistakes 
* Design strategies for mitigating the risks of failures due to ML mistakes


----
## Models make mistakes

<div class="tweet" data-src="https://twitter.com/justbhutani/status/1567226144197607424"></div>


----
## Common excuse: Nobody could have foreseen this...

![Suicide rate of girls rising with the rise of social media](teen-suicide-rate.png)

----
## What responsibility do designers have to anticipate problems?

![Critical headline about predictive policing](predictive-policing.png)


----
## Confounding Variables

![Confounding variable example](confoundingvariables.svg)
<!-- .element: class="plain" -->

----
## Reverse Causality

![Chess](chess.jpg)

Note: (from Prediction Machines, Chapter 6) Early 1980s chess  program learned from Grandmaster games, learned that sacrificing queen would be a winning move, because it was occuring frequently in winning games. Program then started to sacrifice queen early.

----
## Reasons barely matter

No model is every "correct"

Some mistakes are unavoidable

Anticipate the eventual mistake
* Make the system safe despite mistakes
* Consider the rest of the system (software + environment)
* Example: Thermal fuse in smart toaster

**ML model = unreliable component**







----
## Bollards mitigate mistakes

<div class="tweet" data-src="https://twitter.com/WorldBollard/status/1534901378983796736"></div>




----
## Today's Running Example: Autonomous Train

<!-- colstart -->

![Docklands train](dlr.jpg)
<!-- .element: class="stretch" -->

<div class="small">CC BY 2.0 by Matt Brown</div>

<!-- col -->
* REQ: The train shall not collide with obstacles
* REQ: The train shall not depart until all doors are closed
* REQ: The train shall not trap people between the doors
* ...

<!-- colend -->

Note: The Docklands Light Railway system in London has operated trains without a driver since 1987. Many modern public transportation systems use increasingly sophisticated automation, including the Paris Métro Line 14 and the Copenhagen Metro

----
## Human in the Loop - Examples

* Email response suggestions

![Example of email responses suggested by GMail](email.png)

* Fall detection smartwatch
* Safe browsing

----
## Undoable actions - Examples

![Nest thermostat](nest.jpg)
<!-- .element: class="stretch" -->

* Override thermostat setting
* Undo slide design suggestions
* Automated shipment + offering free return shipment
* Appeal process for banned "spammers" or "bots"
* Easy to repair bumpers on autonomous vehicles?

<!-- img: https://unsplash.com/photos/RFAHj4tI37Y -->

----
## Guardrails - Examples

Recall: Thermal fuse in smart toaster

![Thermal fuse](thermalfuse.png)
<!-- .element: class="stretch" -->


+ maximum toasting time + extra heat sensor


----
## Guardrails - Examples

![Metro station Cour Saint-Émilion in Paris with automated platform screen doors that only open when a train is in the station](platformdoors.png)
<!-- .element: class="stretch" -->

<!-- references_ -->

CC BY-SA 4.0 by Chabe01


----
## Mistake detection

Independent mechanism to detect problems (in the real world)


Example: Gyrosensor to detect a train taking a turn too fast

![Train taking a corner](traincorner.jpg)
<!-- .element: class="stretch" -->

----
## Graceful Degradation (Fail-safe)

<video>
    <source data-src="rc-car.mp4" type="video/mp4" />
</video>

* Goal: When a component failure is detected, achieve system 
  safety by reducing functionality and performance
* Switches operating mode when failure detected (e.g., slower, conservative)

----
## Redundancy Example: Sensor Fusion

![](sensor-fusion.jpeg)
<!-- .element: class="stretch" -->

* Combine data from a wide range of sensors
* Provides partial information even when some sensor is faulty
* A critical part of modern self-driving vehicles


----
## Short Breakout

What design strategies would you consider to mitigate ML mistakes:
* Credit card fraud detection
* Image captioning for accessibility in photo sharing site
* Speed limiter for cars (with vision system to detect traffic signs)

Consider: Human in the loop, Undoable actions, Guardrails, Mistake detection and recovery (monitoring, doer-checker, fail-over, redundancy), Containment and isolation


As a group, post one design idea for each scenario to `#lecture` and tag all group members.






----
## What's the worst that could happen?

![Robot uprising](robot-uprising.jpg)<!-- .element: style="width:800px" -->

<!-- references -->

*Likely?* Toby Ord predicts existential risk from GAI at 10% within 100 years:
Toby Ord, "The Precipice: Existential Risk and the Future of Humanity", 2020

Note: Discussion on existential risk. Toby Ord, Oxford philosopher predicts 

----
## What's the worst that could happen?

![Albumy screenshot](albumy.png)
<!-- .element: class="stretch" -->



----
## What is Risk Analysis?

What can possibly go wrong in my system, and what are potential 
impacts on system requirements?

Risk = Likelihood * Impact

A number of methods:
  * Failure mode & effects analysis (FMEA)
  * Hazard analysis
  * Why-because analysis
  * Fault tree analysis (FTA)
  * ...


----
## Fault Tree Analysis (FTA)

<!-- colstart -->

<div class="small">

* Fault tree: A top-down diagram that displays the relationships
between a system failure (i.e., requirement violation) and its potential causes.  
  * Identify sequences of events that result in a failure
  * Prioritize the contributors leading to the failure
  * Inform decisions about how to (re-)design the system
  * Investigate an accident & identify the root cause 
* Often used for safety & reliability, but can also be used for
other types of requirements (e.g., poor performance, security attacks...)

</div>

<!-- col -->

![fta-sample](fta-sample.png)<!-- .element: style="width:400px" -->

<!-- colend -->

----
![FTA for trapping people in doors of a train](fta.svg)

----
## Consider Mitigations

* Remove basic events with mitigations
* Increase the size of cut sets with mitigations


![FTA for trapping people in doors of a train](fta-without-mitigation.svg)
<!-- .element: class="stretch" -->

----
## Failure Mode and Effects Analysis (FMEA)

![](fmea-radiation.png)
<!-- .element: class="stretch" -->

* A __forward search__ technique to identify potential hazards
* Widely used in aeronautics, automotive, healthcare, food services,
  semiconductor processing, and (to some extent) software

----
## Hazard and Interoperability Study (HAZOP)
   
*identify hazards and component fault scenarios through guided inspection of requirements*

![HAZOP example](hazop-perception.jpg)



---
<!-- .element: class="titleslide"  data-background="../_chapterimg/08_architecture.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Toward Architecture and Design



----
## After requirements...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->


----
## Learning Goals

* Describe the role of architecture and design between requirements and implementation
* Identify the different ML components and organize and prioritize their quality concerns for a given project
* Explain they key ideas behind decision trees and random forests and analyze consequences for various qualities
* Demonstrate an understanding of the key ideas of deep learning and how it drives qualities
* Plan and execute an evaluation of the qualities of alternative AI components for a given purpose

----
## Readings

Required reading: Hulten, Geoff. "Building Intelligent Systems: A
Guide to Machine Learning Engineering." (2018), Chapters 17 and 18

Recommended reading: Siebert, Julien, Lisa Joeckel, Jens Heidrich, Koji Nakamichi, Kyoko Ohashi, Isao Namba, Rieko Yamamoto, and Mikio Aoyama. “Towards Guidelines for Assessing Qualities of Machine Learning Systems.” In International Conference on the Quality of Information and Communications Technology, pp. 17–31. Springer, Cham, 2020.













----
<!-- colstart -->
![Simple architecture diagram of transcription service](transcriptionarchitecture2.svg)
<!-- .element: class="plain" -->

<!-- col -->

* **ML components** for transcription model, pipeline to train the model, monitoring infrastructure...
* **Non-ML components** for data storage, user interface, payment processing, ...
* User requirements and assumptions
* 
* System quality vs model quality
* System requirements vs model requirements
 
<!-- colend -->



----
# Thinking like a Software Architect

![Architecture between requirements and implementation](req-arch-impl.svg)
<!-- .element: class="plain" -->


----

## Case Study: Twitter

![twitter](twitter.png)<!-- .element: style="width:800px" -->


Note: Source and additional reading: Raffi. [New Tweets per second record, and how!](https://blog.twitter.com/engineering/en_us/a/2013/new-tweets-per-second-record-and-how.html) Twitter Blog, 2013


----

## Twitter Case Study: Key Insights

Architectural decisions affect entire systems, not only individual modules

Abstract, different abstractions for different scenarios

Reason about quality attributes early

Make architectural decisions explicit

Question: **Did the original architect make poor decisions?**









----
## System Decomposition

![Simple architecture diagram of transcription service](transcriptionarchitecture2.svg)
<!-- .element: class="stretch plain" -->

Identify components and their responsibilities

Establishes interfaces and team boundaries


----
## Information Hiding

Decomposition enables scaling teams

Each team works on a component

Need to coordinate on *interfaces*, but implementations remain hidden

**Interface descriptions are crutial**
* Who is responsible for what
* Component requirements (specifications), behavioral and quality
* Especially consider nonlocal qualities: e.g., safety, privacy

Interfaces rarely fully specified in practice, source of conflicts




----
## Common components

* **Model inference service**: Uses model to make predictions for input data
* **ML pipeline**: Infrastructure to train/update the model
* **Monitoring**: Observe model and system
* **Data sources**: Manual/crowdsourcing/logs/telemetry/...
* **Data management**: Storage and processing of data, often at scale
* **Feature store**: Reusable feature engineering code, cached feature computations

----
## Common System-Wide Design Challenges

Separating concerns, understanding interdependencies
* e.g., anticipating/breaking feedback loops, conflicting needs of components

Facilitating experimentation, updates with confidence

Separating training and inference and closing the loop
* e.g., collecting telemetry to learn from user interactions

Learn, serve, and observe at scale or with resource limits
* e.g., cloud deployment, embedded devices




----
## Qualities of Interest?

Scenario: Component for detecting credit card frauds, as a service for banks

![Credit card](credit-card.jpg)
<!-- .element: class="stretch" -->


Note: Very high volume of transactions, low cost per transaction, frequent updates

Incrementality

<!-- Img src https://pixabay.com/photos/credit-card-payment-transaction-926862/ -->

----
![Table of NFPs and their relationship to different components](nfps.png)
<!-- .element: class="plain stretch" -->

<!-- references_ -->
From: Habibullah, Khan Mohammad, Gregory Gay, and Jennifer Horkoff. "[Non-Functional Requirements for Machine Learning: An Exploration of System Scope and Interest](https://arxiv.org/abs/2203.11063)." arXiv preprint arXiv:2203.11063 (2022).



----
## Decision Trees: Qualities

![Decision tree](decisiontreeexample.png)
<!-- .element: class="stretch" -->
  
* Tasks: Classification & regression
* Qualities: __Advantages__: ??  __Drawbacks__: ??

Notes:
* Easy to interpret (up to a size); can capture non-linearity; can do well with
  little data
* High risk of overfitting; possibly very large tree size
* Obvious ones: fairly small model size, low inference cost, 
no obvious incremental training; easy to interpret locally and 
even globally if shallow; easy to understand decision boundaries

<!-- <\!-- smallish -\-> -->
<!-- * Identify all possible decisions -->
<!-- * Select the decision that best splits the dataset into distinct outcomes (typically via entropy or similar measure) -->
<!-- * Repeatedly further split subsets, until stopping criteria reached -->


----
$f_{\mathbf{W}_h,\mathbf{b}_h,\mathbf{W}_o,\mathbf{b}_o}(\mathbf{X})=\phi( \mathbf{W}_o \cdot \phi(\mathbf{W}_h \cdot \mathbf{X}+\mathbf{b}_h)+\mathbf{b}_o)$

![Multi Layer Perceptron](mlperceptron.svg)
<!-- .element: class="stretch" -->

(matrix multiplications interleaved with step function)


----
## Deep Learning

![neural-network](neural-network.png)

* Tasks: Classification & regression
* Qualities: __Advantages__: ?? __Drawbacks__: ??

Notes:
* High accuracy; can capture a wide range of problems (linear & non-linear)
* Difficult to interpret; high training costs (time & amount of
data required, hyperparameter tuning)

----
## Network Size

<div class="smallish">

* 50 Layer ResNet network -- classifying 224x224 images into 1000 categories
  * 26 million weights, computes 16 million activations during inference, 168 MB to store weights as floats
* Google in 2012(!): 1TB-1PB of training data, 1 billion to 1 trillion parameters
* OpenAI’s GPT-2 (2019) -- text generation
  - 48 layers, 1.5 billion weights (~12 GB to store weights)
  - released model reduced to 117 million weights
  - trained on 7-8 GPUs for 1 month with 40GB of internet text from 8 million web pages
* OpenAI’s GPT-3 (2020): 96 layers, 175 billion weights, 700 GB in memory, $4.6M in approximate compute cost for training
</div>

Notes: https://lambdalabs.com/blog/demystifying-gpt-3/

----
## Cost & Energy Consumption

<div class="smallish">

  <!-- colstart -->

| Consumption | CO2 (lbs) |
| - | - |
| Air travel, 1 passenger, NY↔SF | 1984 |
| Human life, avg, 1 year | 11,023 |
| American life, avg, 1 year | 36,156 |
| Car, avg incl. fuel, 1 lifetime | 126,000 |

<!-- col -->

| Training one model (GPU) | CO2 (lbs) |
| - | - |
| NLP pipeline (parsing, SRL) | 39 |
| w/ tuning & experimentation | 78,468 |
| Transformer (big) | 192 |
| w/ neural architecture search | 626,155 |

<!-- colend -->

</div>

<!-- references -->
Strubell, Emma, Ananya Ganesh, and Andrew McCallum. "[Energy and Policy Considerations for Deep Learning in NLP](https://arxiv.org/pdf/1906.02243.pdf)." In Proc. ACL, pp. 3645-3650. 2019.





----
# Constraints and Tradeoffs

![Pareto Front Example](pareto-front.svg)
<!-- .element: class="stretch plain" -->



----
## Constraints

Constraints define the space of attributes for valid design solutions

![constraints](design-space.svg)
<!-- .element: class="stretch plain" -->

Note: Design space exploration: The space of all possible designs (dotted rectangle) is reduced by several constraints on qualities of the system, leaving only a subset of designs for further consideration (highlighted center area).


----
## Trade-offs: Cost vs Accuracy

<!-- colstart -->

![Netflix prize leaderboard](netflix-leaderboard.png)
<!-- .element: class="stretch" -->

<!-- col -->

_"We evaluated some of the new methods offline but the additional
accuracy gains that we measured did not seem to justify the
engineering effort needed to bring them into a production
environment.”_

<!-- colend -->

<!-- references_ -->

Amatriain & Basilico. [Netflix Recommendations: Beyond the 5 stars](https://netflixtechblog.com/netflix-recommendations-beyond-the-5-stars-part-1-55838468f429),
Netflix Technology Blog (2012)


----
## Breakout: Qualities & ML Algorithms

Consider two scenarios:
1. Credit card fraud detection
2. Pedestrian detection in sidewalk robot

As a group, post to `#lecture` tagging all group members:
>  * Qualities of interests: ??
>  * Constraints: ??
>  * ML algorithm(s) to use: ??





---
<!-- .element: class="titleslide"  data-background="../_chapterimg/09_deployment.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Deploying a Model




----

## Learning Goals

<div class="smallish">

* Understand important quality considerations when deploying ML components
* Follow a design process to explicitly reason about alternative designs and their quality tradeoffs
* Gather data to make informed decisions about what ML technique to use and where and how to deploy it
* Understand the power of design patterns for codifying design knowledge
*
* Create architectural models to reason about relevant characteristics
* Critique the decision of where an AI model lives (e.g., cloud vs edge vs hybrid), considering the relevant tradeoffs 
* Deploy models locally and to the cloud
* Document model inference services

</div>


----
## Deploying a Model is Easy

Model inference component as a service


```python
from flask import Flask, escape, request
app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = '/tmp/uploads'
detector_model = … # load model…

# inference API that returns JSON with classes 
# found in an image
@app.route('/get_objects', methods=['POST'])
def pred():
    uploaded_img = request.files["images"]
    coverted_img = … # feature encoding of uploaded img
    result = detector_model(converted_img)
    return jsonify({"response":
                result['detection_class_entities']})

```






----
## But is it really easy?

Offline use?

Deployment at scale?

Hardware needs and operating cost?

Frequent updates?

Integration of the model into a system?

Meeting system requirements?

**Every system is different!**

----
![](pgh-cycling.jpg)
Notes: Cycling map of Pittsburgh. Abstraction for navigation with bikes and walking.

----
## What can we reason about?

![Apollo Self-Driving Car Architecture](apollo.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Peng, Zi, Jinqiu Yang, Tse-Hsun Chen, and Lei Ma. "A first look at the integration of machine learning models in complex autonomous driving systems: a case study on Apollo." In Proc. FSE, 2020.



----
## Case Study: Augmented Reality Translation
![Google Glasses](googleglasses.jpg)
<!-- .element: class="stretch" -->

Notes: Consider you want to implement an instant translation service similar toGoogle translate, but run it on embedded hardware in glasses as an augmented reality service.

----
## Where Should the Models Live?

![AR Translation Architecture Sketch](ar-architecture.svg)
<!-- .element: class="plain" -->

Cloud? Phone? Glasses?

What qualities are relevant for the decision?

Notes: Trigger initial discussion


----
## Breakout: Latency and Bandwidth Analysis


1. Estimate latency and bandwidth requirements between components
2. Discuss tradeoffs among different deployment models


![AR Translation Architecture Sketch](ar-architecture.svg)
<!-- .element: class="plain stretch" -->


As a group, post in `#lecture` tagging group members:
* Recommended deployment for OCR (with justification):
* Recommended deployment for Translation (with justification):



Notes: Identify at least OCR and Translation service as two AI components in a larger system. Discuss which system components are worth modeling (e.g., rendering, database, support forum). Discuss how to get good estimates for latency and bandwidth.

Some data:
200ms latency is noticable as speech pause; 
20ms is perceivable as video delay, 10ms as haptic delay;
5ms referenced as cybersickness threshold for virtual reality
20ms latency might be acceptable

bluetooth latency around 40ms to 200ms

bluetooth bandwidth up to 3mbit, wifi 54mbit, video stream depending on quality 4 to 10mbit for low to medium quality

google glasses had 5 megapixel camera, 640x360 pixel screen, 1 or 2gb ram, 16gb storage


----
## Reusing Feature Engineering Code


![Feature encoding shared between training and inference](shared-feature-encoding.svg)
<!-- .element: class="plain stretch" -->


Avoid *training–serving skew*

----
## Tecton Feature Store

<iframe width="1200" height="600" src="https://www.youtube.com/embed/u_L_V2HQ_nQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

----
## Separating Models and Business Logic

![3-tier architecture integrating ML](3tier-with-ml.svg)
<!-- .element: class="stretch plain" -->

<!-- references_ -->
Based on: Yokoyama, Haruki. "Machine learning system architectural pattern for improving operational stability." In Int'l Conf. Software Architecture Companion, pp. 267-274. IEEE, 2019.

----
## Documenting Input/Output Types for Inference Components

```js
{
  "mid": string,
  "languageCode": string,
  "name": string,
  "score": number,
  "boundingPoly": {
    object (BoundingPoly)
  }
}
```
From Google’s public [object detection API](https://cloud.google.com/vision/docs/object-localizer).

----
![Model card screenshot from Google](modelcard2.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
From: https://modelcards.withgoogle.com/object-detection


----
## Anti-Patterns

* Big Ass Script Architecture
* Dead Experimental Code Paths
* Glue code
* Multiple Language Smell
* Pipeline Jungles
* Plain-Old Datatype Smell
* Undeclared Consumers



<!-- references -->

See also: 🗎 Washizaki, Hironori, Hiromu Uchida, Foutse Khomh, and Yann-Gaël Guéhéneuc. "[Machine Learning Architecture and Design Patterns](http://www.washi.cs.waseda.ac.jp/wp-content/uploads/2019/12/IEEE_Software_19__ML_Patterns.pdf)." Draft, 2019; 🗎 Sculley, et al. "[Hidden technical debt in machine learning systems](http://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)." In NeurIPS, 2015.





---
<!-- .element: class="titleslide"  data-background="../_chapterimg/10_qainproduction.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Testing in Production


----
<div class="tweet" data-src="https://twitter.com/changelog/status/1137359428632621060"></div>


----
## Learning Goals

* Design telemetry for evaluation in practice
* Understand the rationale for beta tests and chaos experiments
* Plan and execute experiments (chaos, A/B, shadow releases, ...) in production
* Conduct and evaluate multiple concurrent A/B tests in a system
* Perform canary releases
* Examine experimental results with statistical rigor
* Support data scientists with monitoring platforms providing insights from production data

----
## Beta Testing

![Windows 95 beta release](windowsbeta.jpg)
<!-- .element: class="stretch" -->

Note: Early release to select users, asking them to send feedback or report issues. No telemetry in early days.

----
## Crash Telemetry

![Windows 95 Crash Report](wincrashreport_windows_xp.png)<!-- .element: style="width:900px" -->

Note: With internet availability, send crash reports home to identify problems "in production". Most ML-based systems are online in some form and allow telemetry. 

----
## A/B Testing

![A/B test example](ab-groove.jpg)<!-- .element:  style="width:1200px" -->

Notes: Usage observable online, telemetry allows testing in production.  Picture source: https://www.designforfounders.com/ab-testing-examples/


----

<!-- colstart -->
![Skype feedback dialog](skype1.jpg)
<!-- col -->
![Skype report problem button](skype2.jpg)
<!-- colend -->

Notes:
Expect only sparse feedback and expect negative feedback over-proportionally

----
![Flight cost forcast](flightforcast.jpg)<!-- .element:  style="width:840px" -->

Notes: Can just wait 7 days to see actual outcome for all predictions


----
## Measuring Model Quality with Telemetry

<div class="smallish">

* Usual 3 steps: (1) Metric, (2) data collection (telemetry), (3) operationalization
* Telemetry can provide insights for correctness
    - sometimes very accurate labels for real unseen data
    - sometimes only mistakes
    - sometimes delayed
    - often just samples
    - often just weak proxies for correctness
* Often sufficient to *approximate* precision/recall or other model-quality measures
* Mismatch to (static) evaluation set may indicate stale or unrepresentative data
* Trend analysis can provide insights even for inaccurate proxy measures
</div>

----
## Breakout: Design Telemetry in Production

<div class="smallish">

Discuss how to collect telemetry, the metric to monitor, and how to operationalize

Scenarios:
* Front-left: Amazon: Shopping app detects the shoe brand from photos
* Front-right: Google: Tagging uploaded photos with friends' names
* Back-left: Spotify: Recommended personalized playlists
* Back-right: Wordpress: Profanity filter to moderate blog posts

As a group post to `#lecture` and tag team members:
> * Quality metric:
> * Data to collect:
> * Operationalization:

</div>

----
![Grafana screenshot from Movie Recommendation Service](grafana.png)<!-- .element:  style="width:1200px" -->


----
## Detecting Drift

![Drift](drift.jpg)<!-- .element:  style="width:1000px" -->

<!-- references -->
Image source: Joel Thomas and Clemens Mewald. [Productionizing Machine Learning: From Deployment to Drift Detection](https://databricks.com/blog/2019/09/18/productionizing-machine-learning-from-deployment-to-drift-detection.html). Databricks Blog, 2019

----
## Engineering Challenges for Telemetry
![Amazon news story](alexa.png)

----
## Model Quality vs System Quality

![Booking.com homepage](bookingcom.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Bernardi, Lucas, et al. "150 successful machine learning models: 6 lessons learned at Booking.com." In Proc. Int'l Conf. Knowledge Discovery & Data Mining, 2019.


----

<!-- colstart -->
![A/B experiment at Bing](kohavi-bing-search.jpg)

<!-- col -->
<div class="smallish">

## Bing Experiment

* Experiment: Ad Display at Bing
* Suggestion prioritzed low
* Not implemented for 6 month
* Ran A/B test in production
* Within 2h *revenue-too-high* alarm triggered suggesting serious bug (e.g., double billing)
* Revenue increase by 12% - $100M anually in US
* Did not hurt user-experience metrics

</div>

<div class="small">

From: Kohavi, Ron, Diane Tang, and Ya Xu. "[Trustworthy Online Controlled Experiments: A Practical Guide to A/B Testing](https://bookshop.org/books/trustworthy-online-controlled-experiments-a-practical-guide-to-a-b-testing/9781108724265)."  2020.

</div>
<!-- colend -->


----
## Feature Flags (Boolean flags)

<div class="smallish">

```java
if (features.enabled(userId, "one_click_checkout")) {
     // new one click checkout function
} else {
     // old checkout functionality
}
```

* Good practices: tracked explicitly, documented, keep them localized and independent
* External mapping of flags to customers, who should see what configuration
    * e.g., 1% of users sees `one_click_checkout`, but always the same users; or 50% of beta-users and 90% of developers and 0.1% of all users

```scala
def isEnabled(user): Boolean = (hash(user.id) % 100) < 10
```

</div>

----
![t-test in an A/B testing dashboard](testexample.png)
<!-- .element: class="stretch" --> 

<!-- references_ -->
Source: https://conversionsciences.com/ab-testing-statistics/


----
## Canary Releases

<!-- colstart -->

Release new version to small percentage of population (like A/B testing)

Automatically roll back if quality measures degrade

Automatically and incrementally increase deployment to 100% otherwise

<!-- col -->

![Canary bird](canary.jpg)
<!-- .element: class="stretch" -->

<!-- colend -->

----
## Chaos Experiments

[![Simian Army logo by Netflix](simianarmy.jpg)](https://en.wikipedia.org/wiki/Chaos_engineering)
<!-- .element: class="stretch" -->

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/11_infrastructurequality.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Infrastructure Quality & MLOps

<!-- image: https://pixabay.com/photos/lost-places-factory-old-abandoned-1798640/ -->


----

# Learning Goals

* Implement and automate tests for all parts of the ML pipeline
* Understand testing opportunities beyond functional correctness
* Automate test execution with continuous integration
* Deploy a service for models using container infrastructure
* Automate common configuration management tasks
* Devise a monitoring strategy and suggest suitable components for implementing it
* Diagnose common operations problems
* Understand the typical concerns and concepts of MLOps

----
## Possible Mistakes in ML Pipelines

![Pipeline](pipeline.svg)
<!-- .element: class="plain" -->

Danger of "silent" mistakes in many phases

**Examples?**


----
## Integrating the Pipeline with other Components

![Connections between the pipeline and other components](pipeline-connections.svg)
<!-- .element: class="plain" -->


----
## Unit Test, Integration Tests, System Tests

![Testing levels](testinglevels.png)<!-- .element: class="plain" style="width:1200px" -->

Notes:

Software is developed in units that are later assembled. Accordingly we can distinguish different levels of testing.

Unit Testing - A unit is the "smallest" piece of software that a developer creates. It is typically the work of one programmer and is stored in a single file. Different programming languages have different units: In C++ and Java the unit is the class; in C the unit is the function; in less structured languages like Basic and COBOL the unit may be the entire program.

Integration Testing - In integration we assemble units together into subsystems and finally into systems. It is possible for units to function perfectly in isolation but to fail when integrated. For example because they share an area of the computer memory or because the order of invocation of the different methods is not the one anticipated by the different programmers or because there is a mismatch in the data types. Etc.

System Testing - A system consists of all of the software (and possibly hardware, user manuals, training materials, etc.) that make up the product delivered to the customer. System testing focuses on defects that arise at this highest level of integration. Typically system testing includes many types of testing: functionality, usability, security, internationalization and localization, reliability and availability, capacity, performance, backup and recovery, portability, and many more. 

Acceptance Testing - Acceptance testing is defined as that testing, which when completed successfully, will result in the customer accepting the software and giving us their money. From the customer's point of view, they would generally like the most exhaustive acceptance testing possible (equivalent to the level of system testing). From the vendor's point of view, we would generally like the minimum level of testing possible that would result in money changing hands.
Typical strategic questions that should be addressed before acceptance testing are: Who defines the level of the acceptance testing? Who creates the test scripts? Who executes the tests? What is the pass/fail criteria for the acceptance test? When and how do we get paid?


----
## General Testing Strategy: Decoupling Code Under Test

![Test driver-code-stub](driver-stubs-interface.svg)<!-- .element: class="plain" style="width:1200px" -->



----
## Subtle Bugs in Data Wrangling Code


```python
df['Join_year'] = df.Joined.dropna().map(
    lambda x: x.split(',')[1].split(' ')[1])
```
```python
df.loc[idx_nan_age,'Age'].loc[idx_nan_age] = 
    df['Title'].loc[idx_nan_age].map(map_means)
```
```python
df["Weight"].astype(str).astype(int)
```

----
## Modularizing and Testing Data Cleaning

```python
def is_valid_row(row):
    try:
        datetime.strptime(row['date'], '%b %d %Y')
        return true
    except ValueError:
        return false
```

```python
@test
def test_dates(self):
    self.assertTrue(is_valid_row(...))
    self.assertTrue(is_valid_row(...))
    self.assertFalse(is_valid_row(...))
```




----
## Integration and system tests

Test larger units of behavior

Often based on use cases or user stories -- customer perspective

```java
@Test void testCleaningWithFeatureEng() {
    DataFrame d = loadTestData();
    DataFrame cd = clean(d);
    DataFrame f = feature3.encode(cd);
    assert(noMissingValues(f.getColumn("m")));
    assert(max(f.getColumn("m"))<=1.0);
}

```

----
![Code Review on GitHub](review_github.png)

----
## Static Analysis, Code Linting

Automatic detection of problematic patterns based on code structure

```java
if (user.jobTitle = "manager") {
   ...
}
```

```javascript
function fn() {
    x = 1;
    return x;
    x = 3; 
}
```


----
## Breakout Groups

* In the Smartphone Covid Detection scenario
* Discuss in groups:
  * Back left: data tests
  * Back right: model dev. tests
  * Front right: infrastructure tests
  * Front left: monitoring tests
* For 8 min, discuss some of the listed point in the context of the Covid-detection scenario: what would you do?
* In `#lecture`, tagging group members, suggest what tests to implement











----
# Dev vs. Ops

![](devops_meme.jpg)<!-- .element: style="width:700px" -->

----
<!-- colstart -->
## Developers


* Coding
* Testing, static analysis, reviews
* Continuous integration
* Bug tracking
* Running local tests and scalability experiments
* ...

<!-- col -->
## Operations

* Allocating hardware resources
* Managing OS updates
* Monitoring performance
* Monitoring crashes
* Managing load spikes, …
* Tuning database performance
* Running distributed at scale
* Rolling back releases
* ...

<!-- colend -->

QA responsibilities in both roles


----
## Heavy tooling and automation

[![DevOps tooling overview](devops_tools.jpg)](devops_tools.jpg)

----
## Automate Everything

![CD vs CD](continuous_delivery.gif)<!-- .element: style="width:1200px" -->


----
## Containers

<!-- colstart -->
* Lightweight virtual machine
* Contains entire runnable software, incl. all dependencies and configurations
* Used in development and production
* Sub-second launch time
* Explicit control over shared disks and network connections

<!-- col -->
![Docker logo](docker_logo.png)

<!-- colend -->

----

![Kubernetes](Kubernetes.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
CC BY-SA 4.0 [Khtan66](https://en.wikipedia.org/wiki/Kubernetes#/media/File:Kubernetes.png)

----
## MLOps Overview

Integrate ML artifacts into software release process, unify process (i.e., DevOps extension)

Automated data and model validation (continuous deployment)


Continuous deployment for ML models: from experimenting in notebooks to quick feedback in production

Versioning of models and datasets (more later)

Monitoring in production (discussed earlier)


<!-- references -->
Further reading: [MLOps principles
](https://ml-ops.org/content/mlops-principles.html)

----
## Tooling Landscape LF AI

[![LF AI Landscape](lfai-landscape.png)](https://landscape.lfai.foundation/)

<!-- references -->
Linux Foundation AI Initiative


---
<!-- .element: class="titleslide"  data-background="../_chapterimg/12_dataquality.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Data Quality

<!-- image: https://pixabay.com/photos/high-level-rack-warehouse-range-408222/-->




----

## Learning Goals

* Distinguish precision and accuracy; understanding the better models vs more data tradeoffs
* Use schema languages to enforce data schemas
* Design and implement automated quality assurance steps that check data schema conformance and distributions 
* Devise infrastructure for detecting data drift and schema violations
* Consider data quality as part of a system; design an organization that values data quality


----

> Data cleaning and repairing account for about 60% of the work of data scientists.


**Own experience?**


<!-- references -->
Quote: Gil Press. “[Cleaning Big Data: Most Time-Consuming, Least Enjoyable Data Science Task, Survey Says](https://www.forbes.com/sites/gilpress/2016/03/23/data-preparation-most-time-consuming-least-enjoyable-data-science-task-survey-says/).” Forbes Magazine, 2016.


----
## Case Study: Inventory Management

![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->


----
## Many Data Sources

<svg id="mermaid1" width="100%" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" height="300.4444580078125" style="max-width: 974.0121459960938px;" viewBox="0 0.0000019073486328125 974.0121459960938 300.4444580078125"><style>#mermaid1 {font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid1 .error-icon{fill:#552222;}#mermaid1 .error-text{fill:#552222;stroke:#552222;}#mermaid1 .edge-thickness-normal{stroke-width:2px;}#mermaid1 .edge-thickness-thick{stroke-width:3.5px;}#mermaid1 .edge-pattern-solid{stroke-dasharray:0;}#mermaid1 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid1 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid1 .marker{fill:#333333;stroke:#333333;}#mermaid1 .marker.cross{stroke:#333333;}#mermaid1 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid1 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid1 .cluster-label text{fill:#333;}#mermaid1 .cluster-label span{color:#333;}#mermaid1 .label text,#mermaid1 span{fill:#333;color:#333;}#mermaid1 .node rect,#mermaid1 .node circle,#mermaid1 .node ellipse,#mermaid1 .node polygon,#mermaid1 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid1 .node .label{text-align:center;}#mermaid1 .node.clickable{cursor:pointer;}#mermaid1 .arrowheadPath{fill:#333333;}#mermaid1 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid1 .flowchart-link{stroke:#333333;fill:none;}#mermaid1 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid1 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid1 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid1 .cluster text{fill:#333;}#mermaid1 .cluster span{color:#333;}#mermaid1 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid1 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}</style><g><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath LS-Twitter LE-SalesTrends" style="opacity: 1;" id="L-Twitter-SalesTrends"><path class="path" d="M41.55034637451172,44.0069465637207L41.55034637451172,48.17361323038737C41.55034637451172,52.34027989705404,41.55034637451172,60.67361323038737,48.17041761636077,69.0069465637207C54.790488858209834,77.34027989705403,68.03063134190793,85.67361323038737,74.650702583757,89.84027989705403L81.27077382560604,94.0069465637207" marker-end="url(#arrowhead18)" style="fill:none"></path><defs><marker id="arrowhead18" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-AdNetworks LE-SalesTrends" style="opacity: 1;" id="L-AdNetworks-SalesTrends"><path class="path" d="M178.19965362548828,44.0069465637207L178.19965362548828,48.17361323038737C178.19965362548828,52.34027989705404,178.19965362548828,60.67361323038737,171.57958238363923,69.0069465637207C164.95951114179016,77.34027989705403,151.71936865809207,85.67361323038737,145.09929741624302,89.84027989705403L138.47922617439397,94.0069465637207" marker-end="url(#arrowhead19)" style="fill:none"></path><defs><marker id="arrowhead19" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-SalesTrends LE-Prediction" style="opacity: 1;" id="L-SalesTrends-Prediction"><path class="path" d="M109.875,130.0138931274414L109.875,134.18055979410806C109.875,138.34722646077475,109.875,146.68055979410806,166.44622099680836,162.49383973114013C223.0174419936167,178.3071196681722,336.1598839872334,201.600346208903,392.7311049840417,213.24695947926838L449.30232598085007,224.8935727496338" marker-end="url(#arrowhead20)" style="fill:none"></path><defs><marker id="arrowhead20" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-VendorSales LE-Prediction" style="opacity: 1;" id="L-VendorSales-Prediction"><path class="path" d="M269.80555725097656,130.0138931274414L269.80555725097656,134.18055979410806C269.80555725097656,138.34722646077475,269.80555725097656,146.68055979410806,300.0449251591014,161.31758370019978C330.28429306722626,175.9546076062915,390.76302888347595,196.89532208514163,421.0023967916008,207.36567932456668L451.24176469972565,217.83603656399174" marker-end="url(#arrowhead21)" style="fill:none"></path><defs><marker id="arrowhead21" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-ProductData LE-Prediction" style="opacity: 1;" id="L-ProductData-Prediction"><path class="path" d="M429.5885467529297,130.0138931274414L429.5885467529297,134.18055979410806C429.5885467529297,138.34722646077475,429.5885467529297,146.68055979410806,435.70485924925265,157.49039096221438C441.82117174557567,168.30022213032066,454.0537967382217,181.58655113319992,460.17010923454467,188.22971563463955L466.28642173086763,194.87288013607917" marker-end="url(#arrowhead22)" style="fill:none"></path><defs><marker id="arrowhead22" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-Marketing LE-Prediction" style="opacity: 1;" id="L-Marketing-Prediction"><path class="path" d="M579.1371612548828,130.0138931274414L579.1371612548828,134.18055979410806C579.1371612548828,138.34722646077475,579.1371612548828,146.68055979410806,573.0208487585599,157.49039096221438C566.9045362622369,168.30022213032066,554.6719112695909,181.58655113319992,548.5555987732679,188.22971563463955L542.4392862769449,194.87288013607917" marker-end="url(#arrowhead23)" style="fill:none"></path><defs><marker id="arrowhead23" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-Theft LE-Prediction" style="opacity: 1;" id="L-Theft-Prediction"><path class="path" d="M749.1284828186035,130.0138931274414L749.1284828186035,134.18055979410806C749.1284828186035,138.34722646077475,749.1284828186035,146.68055979410806,717.2266872301142,161.43250851168727C685.324891641625,176.18445722926649,621.5213004646463,197.3550213310915,589.619504876157,207.94030338200403L557.7177092876676,218.52558543291656" marker-end="url(#arrowhead24)" style="fill:none"></path><defs><marker id="arrowhead24" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-PastSales LE-Prediction" style="opacity: 1;" id="L-PastSales-Prediction"><path class="path" d="M920.0139007568359,130.0138931274414L920.0139007568359,134.18055979410806C920.0139007568359,138.34722646077475,920.0139007568359,146.68055979410806,859.9340521287166,162.58640451464422C799.8542035005972,178.49224923518037,679.6945062443584,201.97060534291936,619.6146576162391,213.70978339678882L559.5348089881197,225.44896145065835" marker-end="url(#arrowhead25)" style="fill:none"></path><defs><marker id="arrowhead25" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-Twitter-SalesTrends" class="edgeLabel L-LS-Twitter' L-LE-SalesTrends"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-AdNetworks-SalesTrends" class="edgeLabel L-LS-AdNetworks' L-LE-SalesTrends"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-SalesTrends-Prediction" class="edgeLabel L-LS-SalesTrends' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-VendorSales-Prediction" class="edgeLabel L-LS-VendorSales' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-ProductData-Prediction" class="edgeLabel L-LS-ProductData' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-Marketing-Prediction" class="edgeLabel L-LS-Marketing' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-Theft-Prediction" class="edgeLabel L-LS-Theft' L-LE-Prediction"></span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform=""><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-PastSales-Prediction" class="edgeLabel L-LS-PastSales' L-LE-Prediction"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node default" style="opacity: 1;" id="flowchart-Twitter-16" transform="translate(41.55034637451172,26.00347328186035)"><rect rx="0" ry="0" x="-33.55034828186035" y="-18.003472328186035" width="67.1006965637207" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-23.55034828186035,-8.003472328186035)"><foreignObject width="47.1006965637207" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Twitter</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-SalesTrends-17" transform="translate(109.875,112.01041984558105)"><rect rx="0" ry="0" x="-54.59201431274414" y="-18.003472328186035" width="109.18402862548828" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-44.59201431274414,-8.003472328186035)"><foreignObject width="89.18402862548828" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">SalesTrends</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-AdNetworks-18" transform="translate(178.19965362548828,26.00347328186035)"><rect rx="0" ry="0" x="-53.098960876464844" y="-18.003472328186035" width="106.19792175292969" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-43.098960876464844,-8.003472328186035)"><foreignObject width="86.19792175292969" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">AdNetworks</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-Prediction-21" transform="translate(504.36285400390625,236.2291717529297)"><circle x="-56.21527862548828" y="-18.003472328186035" r="56.21527862548828" class="label-container"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-46.21527862548828,-8.003472328186035)"><foreignObject width="92.43055725097656" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Inventory ML</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-VendorSales-22" transform="translate(269.80555725097656,112.01041984558105)"><rect rx="0" ry="0" x="-55.33854293823242" y="-18.003472328186035" width="110.67708587646484" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-45.33854293823242,-8.003472328186035)"><foreignObject width="90.67708587646484" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">VendorSales</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-ProductData-24" transform="translate(429.5885467529297,112.01041984558105)"><rect rx="0" ry="0" x="-54.4444465637207" y="-18.003472328186035" width="108.8888931274414" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-44.4444465637207,-8.003472328186035)"><foreignObject width="88.8888931274414" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">ProductData</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-Marketing-26" transform="translate(579.1371612548828,112.01041984558105)"><rect rx="0" ry="0" x="-45.10416793823242" y="-18.003472328186035" width="90.20833587646484" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-35.10416793823242,-8.003472328186035)"><foreignObject width="70.20833587646484" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Marketing</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-Theft-28" transform="translate(749.1284828186035,112.01041984558105)"><rect rx="0" ry="0" x="-74.88715362548828" y="-18.003472328186035" width="149.77430725097656" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-64.88715362548828,-8.003472328186035)"><foreignObject width="129.77430725097656" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Expired/Lost/Theft</div></foreignObject></g></g></g><g class="node default" style="opacity: 1;" id="flowchart-PastSales-30" transform="translate(920.0139007568359,112.01041984558105)"><rect rx="0" ry="0" x="-45.99826431274414" y="-18.003472328186035" width="91.99652862548828" height="36.00694465637207" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-35.99826431274414,-8.003472328186035)"><foreignObject width="71.99652862548828" height="16.00694465637207"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">PastSales</div></foreignObject></g></g></g></g></g></g></svg>

*sources of different reliability and quality*


----
## *Raw Data* is an Oxymoron

![shipment receipt form](shipment-delivery-receipt.jpg)
<!-- .element: class="stretch" -->



<!-- references_ -->
Recommended Reading: Gitelman, Lisa, Virginia Jackson, Daniel Rosenberg, Travis D. Williams, Kevin R. Brine, Mary Poovey, Matthew Stanley et al. "[Data bite man: The work of sustaining a long-term study](https://ieeexplore.ieee.org/abstract/document/6462156)." In "Raw Data" Is an Oxymoron, (2013), MIT Press: 147-166.

----
## Accuracy vs Precision

<!-- colstart -->

Accuracy: Reported values (on average) represent real value

Precision: Repeated measurements yield the same result

Accurate, but imprecise: Average over multiple measurements

Inaccurate, but precise: ?

<!-- col -->


![Accuracy-vs-precision visualized](Accuracy_and_Precision.svg)<!-- .element: style="width:400px" -->


<!-- colend -->

<!-- references_ -->
(CC-BY-4.0 by [Arbeck](https://commons.wikimedia.org/wiki/File:Accuracy_and_Precision.svg))


----
## Data Cascades

![Data cascades figure](datacascades.png)

Detection almost always delayed! Expensive rework.
Difficult to detect in offline evaluation.

<!-- references -->
Sambasivan, N., et al. (2021, May). “[Everyone wants to do the model work, not the data work”: Data Cascades in High-Stakes AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518). In Proc. CHI (pp. 1-15).




----
## Schema in Relational Databases

```sql
CREATE TABLE employees (
    emp_no      INT             NOT NULL,
    birth_date  DATE            NOT NULL,
    name        VARCHAR(30)     NOT NULL,
    PRIMARY KEY (emp_no));
CREATE TABLE departments (
    dept_no     CHAR(4)         NOT NULL,
    dept_name   VARCHAR(40)     NOT NULL,
    PRIMARY KEY (dept_no), UNIQUE  KEY (dept_name));
CREATE TABLE dept_manager (
   dept_no      CHAR(4)         NOT NULL,
   emp_no       INT             NOT NULL,
   FOREIGN KEY (emp_no)  REFERENCES employees (emp_no),
   FOREIGN KEY (dept_no) REFERENCES departments (dept_no),
   PRIMARY KEY (emp_no,dept_no)); 
```



----
## Example: HoloClean

![HoloClean](holoclean.jpg)
<!-- .element: class="stretch" -->

<div class="small">

* User provides rules as integrity constraints (e.g., "two entries with the same
name can't have different city")
* Detect violations of the rules in the data; also detect statistical outliers
* Automatically generate repair candidates (with probabilities)
</div>

<!-- references_ -->
Image source: Theo Rekatsinas, Ihab Ilyas, and Chris Ré, “[HoloClean - Weakly Supervised Data Repairing](https://dawn.cs.stanford.edu/2017/05/12/holoclean/).” Blog, 2017.

----


## Drift & Model Decay

<div class="small">

**Concept drift** (or concept shift)
  * properties to predict change over time (e.g., what is credit card fraud)
  * model has not learned the relevant concepts
  * over time: different expected outputs for same inputs
  
**Data drift** (or covariate shift, distribution shift, or population drift)
  * characteristics of input data changes (e.g., customers with face masks)
  * input data differs from training data 
  * over time: predictions less confident, further from training data

**Upstream data changes**
  * external changes in data pipeline (e.g., format changes in weather service)
  * model interprets input data incorrectly
  * over time: abrupt changes due to faulty inputs

**How do we fix these drifts?**

</div>
Notes:
  * fix1: retrain with new training data or relabeled old training data
  * fix2: retrain with new data
  * fix3: fix pipeline, retrain entirely

----
## Breakout: Drift in the Inventory System

*What kind of drift might be expected?*

As a group, tagging members, write plausible examples in `#lecture`:

> * Concept Drift:
> * Data Drift:
> * Upstream data changes:


![Shelves in a warehouse](warehouse.jpg)
<!-- .element: class="stretch" -->





----
## Microsoft Azure Data Drift Dashboard

![Dashboard](drift-ui-expanded.png)

<!-- references -->
Image source and further readings: [Detect data drift (preview) on models deployed to Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-monitor-datasets?tabs=python)



----

> "Everyone wants to do the model work, not the data work"

<!-- references -->
Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021, May). “[Everyone wants to do the model work, not the data work”: Data Cascades in High-Stakes AI](https://dl.acm.org/doi/abs/10.1145/3411764.3445518). In Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems (pp. 1-15).

----
## Data Quality Documentation

<div class="smallish">

Teams rarely document expectations of data quantity or quality

Data quality tests are rare, but some teams adopt defensive monitoring
* Local tests about assumed structure and distribution of data
* Identify drift early and reach out to producing teams

Several ideas for documenting distributions, including [Datasheets](https://dl.acm.org/doi/fullHtml/10.1145/3458723) and [Dataset Nutrition Label](https://arxiv.org/abs/1805.03677)
* Mostly focused on static datasets, describing origin, consideration, labeling procedure, and distributions; [Example](https://dl.acm.org/doi/10.1145/3458723#sec-supp)

</div>

<!-- references -->
🗎 Gebru, Timnit, et al. "[Datasheets for datasets](https://dl.acm.org/doi/fullHtml/10.1145/3458723)." Communications of the ACM 64, no. 12 (2021). <br />
🗎 Nahar, Nadia, et al. “[Collaboration Challenges in Building ML-Enabled Systems: Communication, Documentation, Engineering, and Process](https://arxiv.org/abs/2110.10234).” In Pro. ICSE, 2022.

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/13_dataatscale.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Scaling Data Storage and Data Processing



----

# Learning Goals

* Organize different data management solutions and their tradeoffs
* Understand the scalability challenges involved in large-scale machine learning and specifically deep learning
* Explain the tradeoffs between batch processing and stream processing and the lambda architecture
* Recommend and justify a design and corresponding technologies for a given system

----
## Scaling Computations

<!-- colstart -->
Efficent Algorithms
<!-- col -->
Faster Machines
<!-- col -->
More Machines
<!-- colend -->

----
## Distributed Gradient Descent

[![Parameter Server](parameterserver.png)](https://www.usenix.org/system/files/conference/osdi14/osdi14-paper-li_mu.pdf)
<!-- .element: class="stretch" -->

----
## Relational Data Models

<div class="smaller">

**Photos:** 

|photo_id|user_id|path|upload_date|size|camera_id|camera_setting|
|-|-|-|-|-|-|-|
|133422131|54351|/st/u211/1U6uFl47Fy.jpg|2021-12-03T09:18:32.124Z|5.7|663|ƒ/1.8; 1/120; 4.44mm; ISO271|
|133422132|13221| /st/u11b/MFxlL1FY8V.jpg |2021-12-03T09:18:32.129Z|3.1|1844|ƒ/2, 1/15, 3.64mm, ISO1250|
|133422133|54351|/st/x81/ITzhcSmv9s.jpg|2021-12-03T09:18:32.131Z|4.8|663|ƒ/1.8; 1/120; 4.44mm; ISO48|

<!-- colstart -->

**Users:**


| user_id |account_name|photos_total|last_login|
|-|-|-|-|
|54351| ckaestne | 5124 | 2021-12-08T12:27:48.497Z |
|13221| eva.burk     |3|2021-12-21T01:51:54.713Z|

<!-- col -->

**Cameras:**


| camera_id |manufacturer|print_name|
|-|-|-|
|663| Google | Google Pixel 5 |
|1844|Motorola|Motorola MotoG3|

<!-- colend -->

```sql
select p.photo_id, p.path, u.photos_total 
from photos p, users u 
where u.user_id=p.user_id and u.account_name = "ckaestne"
```

</div>

----
## Partitioning

<!-- colstart -->
Divide data:

* *Horizontal partitioning:* Different rows in different tables; e.g., movies by decade, hashing often used
* *Vertical partitioning:* Different columns in different tables; e.g., movie title vs. all actors

**Tradeoffs?**

<!-- col -->

![Horizontal partitioning](horizonalpartition.svg)
<!-- .element: class="plain" -->

<!-- colend -->

----
## Replication with Leaders and Followers

![Leader-follower replication](leaderfollowerreplication.svg)
<!-- .element: class="plain stretch" -->

----
## Microservices

![Audible example](microservice.svg)
<!-- .element: class="plain stretch" -->

<!-- references_ -->
Figure based on Christopher Meiklejohn. [Dynamic Reduction: Optimizing Service-level Fault Injection Testing With Service Encapsulation](http://christophermeiklejohn.com/filibuster/2021/10/14/filibuster-4.html). Blog Post 2021

----
[![Map Reduce example](mapreduce.svg)](mapreduce.svg)
<!-- .element: class="stretch plain" -->

----
## Stream Processing (e.g., Kafka)
![Stream example](stream.svg)
<!-- .element: class="stretch plain" -->

----
## Event Sourcing

* Append only databases
* Record edit events, never mutate data
* Compute current state from all past events, can reconstruct old state
* For efficiency, take state snapshots
* *Similar to traditional database logs, but persistent*

```text
addPhoto(id=133422131, user=54351, path="/st/u211/1U6uFl47Fy.jpg", date="2021-12-03T09:18:32.124Z")
updatePhotoData(id=133422131, user=54351, title="Sunset")
replacePhoto(id=133422131, user=54351, path="/st/x594/vipxBMFlLF.jpg", operation="/filter/palma")
deletePhoto(id=133422131, user=54351)
```

----
## Lambda Architecture and Machine Learning

![Lambda Architecture](lambda.svg)
<!-- .element: class="stretch plain" -->


* Learn accurate model in batch job
* Learn incremental model in stream processor

----
## Data Lake

Trend to store all events in raw form (no consistent schema)

May be useful later

Data storage is comparably cheap

Bet: *Yet unknown future value of data is greater than storage costs*

----
# Breakout: Vimeo Videos

As a group, discuss and post in `#lecture`, tagging group members:
* How to distribute storage:
* How to design scalable copy-right protection solution:
* How to design scalable analytics (views, ratings, ...):

[![Vimeo page](vimeo.png)](https://vimeo.com/about)



---
<!-- .element: class="titleslide"  data-background="../_chapterimg/14_process.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Process and Technical Debt




----
## Process...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->



----

## Learning Goals

<div class="smallish">


* Overview of common data science workflows (e.g., CRISP-DM)
  * Importance of iteration and experimentation
  * Role of computational notebooks in supporting data science workflows
* Overview of software engineering processes and lifecycles: costs and benefits of process, common process models, role of iteration and experimentation
* Contrasting data science and software engineering processes, goals and conflicts
* Integrating data science and software engineering workflows in process model for engineering AI-enabled systems with ML and non-ML components; contrasting different kinds of AI-enabled systems with data science trajectories
* Overview of technical debt as metaphor for process management; common sources of technical debt in AI-enabled systems

</div>

----
## Case Study: Real-Estate Website

![Zillow front page](zillow_main.png)
<!-- .element: class="stretch" -->

----
## Data Science is Iterative and Exploratory


![CRISP-DM](crispdm.png)
<!-- .element: class="stretch plain" -->


<!-- references_ -->
Martínez-Plumed et al. "[CRISP-DM Twenty Years Later: From Data Mining Processes to Data Science Trajectories](https://research-information.bris.ac.uk/files/220614618/TKDE_Data_Science_Trajectories_PF.pdf)." IEEE Transactions on Knowledge and Data Engineering (2019).

----
## Computational Notebooks

<!-- colstart -->

<div class="smallish">

* Origins in "literate programming", interleaving text and code, treating programs as literature (Knuth'84)
* First notebook in Wolfram Mathematica 1.0 in 1988
* Document with text and code cells, showing execution results under cells
* Code of cells is executed, per cell, in a kernel
* Many notebook implementations and supported languages, Python + Jupyter currently most popular

</div>

<!-- col -->

![Notebook example](notebook-example.png)


<!-- colend -->

Notes:
* See also https://en.wikipedia.org/wiki/Literate_programming
* Demo with public notebook, e.g., https://colab.research.google.com/notebooks/mlcc/intro_to_pandas.ipynb

----
![full](process4.png)

Notes: Real experience if little attention is payed to process: increasingly complicated, increasing rework; attempts to rescue by introducing process


----
## Waterfall Model


![Waterfall model](waterfall.svg)
<!-- .element: class="stretch plain" -->

*taming chaos, understand req., plan before coding, remember testing*


Notes: Although dated, the key idea is still essential -- think and plan before implementing. Not all requirements and design can be made upfront, but planning is usually helpful.

----
## Risk First: Spiral Model

![Spiral model](spiral_model.svg)
<!-- .element: class="stretch plain" -->

*incremental prototypes, starting with most risky components*

----
## Constant iteration: Agile

![Scrum Process](scrum.svg)
<!-- .element: class="stretch plain" -->

*working with customers, constant replanning*

<!-- references_ -->
(Image CC BY-SA 4.0, Lakeworks)


----
## Discussion: Iteration in Notebook vs Agile?

<!-- colstart -->
[![Experimental results showing incremental accuracy improvement](accuracy-improvements.png)](accuracy-improvements.png)
<!-- col -->
![Scrum Process](scrum.svg)

<!-- references_ -->
(CC BY-SA 4.0, Lakeworks)
<!-- colend -->

----
## Model first vs Product first

![Combined process](combinedprocess5.svg)
<!-- .element: class="stretch plain" -->



----
# Technical debt


[![](debt.png)](https://www.monkeyuser.com/2018/tech-debt/) 
<!-- .element: class="stretch" -->

----
![Technical Debt Quadrant](techDebtQuadrant.png)<!-- .element: class="plain" style="width:880px" -->

<!-- references -->
Source: Martin Fowler 2009, https://martinfowler.com/bliki/TechnicalDebtQuadrant.html


----
## Breakout: Technical Debt from ML

As a group in `#lecture`, tagging members: Post two plausible examples technical debt in housing price prediction system:
  1. Deliberate, prudent:
  2. Reckless, inadvertent:

![Zillow](zillow_main.png)


<!-- references -->
Sculley, David, et al. [Hidden technical debt in machine learning systems](http://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf). Advances in Neural Information Processing Systems. 2015.
---
<!-- .element: class="titleslide"  data-background="../_chapterimg/15_responsible.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Responsible ML Engineering

(Intro to Ethics and Fairness)






----
## Changing directions...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->



----
## With a few lines of code...

![News headline about airlines splitting up passengers seating](airline.png)

----

<!-- colstart -->

![Martin Shkreli](Martin_Shkreli_2016.jpg)

<!-- col -->

<div class="smallish">

*In 2015, Shkreli received widespread criticism [...] obtained the manufacturing license for the antiparasitic drug Daraprim and raised its price from USD 13.5 to 750 per pill [...] referred to by the media as "the most hated man in America" and "Pharma Bro".* -- [Wikipedia](https://en.wikipedia.org/wiki/Martin_Shkreli)

"*I could have raised it higher and made more profits for our shareholders. Which is my primary duty.*" -- Martin Shkreli

</div>
<!-- colend -->

Note: Image source: https://en.wikipedia.org/wiki/Martin_Shkreli#/media/File:Martin_Shkreli_2016.jpg


----
## Another Example: Social Media

![zuckerberg](mark-zuckerberg.png)
<!-- .element: class="stretch" -->

*What is the (real) organizational objective of the company?*

----
## Mental Health

![teen-suicide-rate](teen-suicide-rate.png)
<!-- .element: class="stretch" -->

* 35% of US teenagers with low social-emotional well-being have been bullied on social media.
* 70% of teens feel excluded when using social media.

<!-- references_ -->
https://leftronic.com/social-media-addiction-statistics

----
## Who's to blame?

![dont-be-evil](dont-be-evil.png)
<!-- .element: class="stretch" -->

*Are these companies intentionally trying to cause harm? If not,
  what are the root causes of the problem?*


----
## Liability?

> THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Note: Software companies have usually gotten away with claiming no liability for their products

----
## Buzzword or real progress?

![Microsoft responsible AI principles](responsibleai.png)
<!-- .element: class="stretch" -->


----
## Legally protected classes (US)

<div class="small">

- Race ([Civil Rights Act of 1964](https://en.wikipedia.org/wiki/Civil_Rights_Act_of_1964))
- Religion ([Civil Rights Act of 1964](https://en.wikipedia.org/wiki/Civil_Rights_Act_of_1964))
- National origin ([Civil Rights Act of 1964](https://en.wikipedia.org/wiki/Civil_Rights_Act_of_1964))
- Sex, sexual orientation, and gender identity ([Equal Pay Act of 1963](https://en.wikipedia.org/wiki/Equal_Pay_Act_of_1963), [Civil Rights Act of 1964](https://en.wikipedia.org/wiki/Civil_Rights_Act_of_1964), and [Bostock v. Clayton](https://en.wikipedia.org/wiki/Bostock_v._Clayton_County))
- Age (40 and over, [Age Discrimination in Employment Act of 1967](https://en.wikipedia.org/wiki/Age_Discrimination_in_Employment_Act_of_1967))
- Pregnancy ([Pregnancy Discrimination Act of 1978](https://en.wikipedia.org/wiki/Pregnancy_Discrimination_Act))
- Familial status (preference for or against having children, [Civil Rights Act of 1968](https://en.wikipedia.org/wiki/Civil_Rights_Act_of_1968))
- Disability status ([Rehabilitation Act of 1973](https://en.wikipedia.org/wiki/Rehabilitation_Act_of_1973); [Americans with Disabilities Act of 1990](https://en.wikipedia.org/wiki/Americans_with_Disabilities_Act_of_1990))
- Veteran status ([Vietnam Era Veterans’ Readjustment Assistance Act of 1974](https://en.wikipedia.org/wiki/Vietnam_Era_Veterans'_Readjustment_Assistance_Act); [Uniformed Services Employment and Reemployment Rights Act of 1994](https://en.wikipedia.org/wiki/Uniformed_Services_Employment_and_Re-employment_Rights_Act_of_1994))
- Genetic information ([Genetic Information Nondiscrimination Act of 2008](https://en.wikipedia.org/wiki/Genetic_Information_Nondiscrimination_Act))

</div>

<!-- references -->

https://en.wikipedia.org/wiki/Protected_group


----
## Dividing a Pie?

<!-- colstart -->


* Equal slices for everybody
* Bigger slices for active bakers
* Bigger slices for inexperienced/new members (e.g., children)
* Bigger slices for hungry people
* More pie for everybody, bake more

*(Not everybody contributed equally during baking, not everybody is equally hungry)*


<!-- col -->

![Pie](../_chapterimg/16_fairness.jpg)

<!-- colend -->

----
## Harms of Allocation

* Withhold opportunities or resources
* Poor quality of service, degraded user experience for certain groups

![](gender-detection.png)
<!-- .element: class="stretch" -->

<!-- references_ -->

_Gender Shades: Intersectional Accuracy Disparities in
Commercial Gender Classification_, Buolamwini & Gebru, ACM FAT* (2018).

----
## Harms of Representation

* Over/under-representation of certain groups in organizations 
* Reinforcement of stereotypes

![](online-ad.png)
<!-- .element: class="stretch" -->

<!-- references_ -->

_Discrimination in Online Ad Delivery_, Latanya Sweeney, SSRN (2013).

----
## Historical Bias

*Data reflects past biases, not intended outcomes*

![Image search for "CEO"](ceo.png)
<!-- .element: class="stretch" -->

*Should the algorithm reflect the reality?*

Note: "An example of this type of bias can be found in a 2018 image search
result where searching for women CEOs ultimately resulted in fewer female CEO images due
to the fact that only 5% of Fortune 500 CEOs were woman—which would cause the search
results to be biased towards male CEOs. These search results were of course reflecting
the reality, but whether or not the search algorithms should reflect this reality is an issue worth
considering."

----
## Tainted Labels

*Bias in dataset labels assigned (directly or indirectly) by humans*

![](amazon-hiring.png)
<!-- .element: class="stretch" -->

Example: Hiring decision dataset -- labels assigned by (possibly biased) experts or derived from past (possibly biased) hiring decisions 

----
## Skewed Sample

*Bias in how and what data is collected*

![](crime-map.jpg)
<!-- .element: class="stretch" -->

Crime prediction: Where to analyze crime? What is considered crime? Actually a random/representative sample?

Recall: Raw data is an oxymoron


----
## Proxies

*Features correlate with protected attribute, remain after removal*
<!-- .element: class="stretch" -->

![](neighborhoods.png)
<!-- .element: class="stretch" -->

* Example: Neighborhood as a proxy for race
* Extracurricular activities as proxy for gender and social class (e.g., “cheerleading”, “peer-mentor for ...”, “sailing team”, “classical music”) 


----
## Feedback Loops reinforce Bias

![Feedback loop](feedbackloop.svg)
<!-- .element: class="stretch plain" -->



> "Big Data processes codify the past.  They do not invent the future.  Doing that requires moral imagination, and that’s something only humans can provide. " -- Cathy O'Neil in [Weapons of Math Destruction](https://cmu.primo.exlibrisgroup.com/permalink/01CMU_INST/6lpsnm/alma991016462699704436)

----
## Breakout: College Admission

Scenario: Evaluate applications & identify students who are 
likely to succeed

Features: GPA, GRE/SAT, gender, race, undergrad institute, alumni
  connections, household income, hometown, transcript, etc.

As a group, post to `#lecture` tagging members:
  * **Possible harms:** Allocation of resources? Quality of service? Stereotyping? Denigration? Over-/Under-representation?
  * **Sources of bias:** Skewed sample? Tainted labels? Historical bias? Limited features?
  Sample size disparity? Proxies?

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/16_fairness.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Measuring Fairness



----
# Learning Goals

* Understand different definitions of fairness
* Discuss methods for measuring fairness
* Outline interventions to improve fairness at the model level

----
## Past bias, different starting positions

![Severe median income and worth disparities between white and black households](mortgage.png)

<!-- references -->
Source: Federal Reserve’s [Survey of Consumer Finances](https://www.federalreserve.gov/econres/scfindex.htm)

----
## Anti-Classification


![](justice.jpeg)
<!-- .element: class="stretch" -->


* Also called _fairness through blindness_ or _fairness through unawareness_
* Ignore certain sensitive attributes when making a decision
* Example: Remove gender and race from mortgage model
* *Easy to implement, but any limitations?*

----
## Group fairness

Key idea: Compare outcomes across two groups
* Similar rates of accepted loans across racial/gender groups?
* Similar chance of being hired/promoted between gender groups?
* Similar rates of (predicted) recidivism across racial groups?

Outcomes matter, not accuracy!

----
## Equalized odds

Key idea: Focus on accuracy (not outcomes) across two groups

* Similar default rates on accepted loans across racial/gender groups?
* Similar rate of "bad hires" and "missed stars" between gender groups?
* Similar accuracy of predicted recidivism vs actual recidivism across racial groups?

Accuracy matters, not outcomes!

----
# Breakout: Cancer Prognosis

![](cancer-stats.png)

In groups, post to `#lecture` tagging members:

* Does the model meet anti-classification fairness wrt. sex?
* Does the model meet group fairness?
* Does the model meet equalized odds?
* Is the model fair enough to use?  


----
## Intuitive Justice

Research on what post people perceive as fair/just (psychology)

When rewards depend on inputs and participants can chose contributions: Most people find it fair to split rewards proportional to inputs
* *Which fairness measure does this relate to?*

Most people agree that for a decision to be fair, personal characteristics that do not influence the reward, such as sex or age, should not be considered when dividing the rewards. 
* *Which fairness measure does this relate to?*

----
## Equality vs Equity

![Contrasting equality, equity, and justice](eej2.jpeg)
<!-- .element: class="stretch" -->

----
![](fairness_tree.png)
<!-- .element: class="stretch" -->

<!-- references_ -->

🕮 Ian Foster, Rayid Ghani, Ron S. Jarmin, Frauke Kreuter and Julia Lane. [Big Data and Social Science: Data Science Methods and Tools for Research and Practice](https://textbook.coleridgeinitiative.org/). Chapter 11, 2nd ed, 2020

----
## Discussion: Fairness Goal for College Admission?

Strong legal precedents

Very limited scope of *affirmative action*

Most forms of group fairness likely illegal

In practice: Anti-classification





----
# Improving Fairness of a Model

In all pipeline stages:
* Data collection
* Data cleaning, processing
* Training
* Inference
* Evaluation and auditing



----
## Example audit tool: Aequitas

![](aequitas-report.png)
<!-- .element: class="stretch" -->

----
## Example: Tweaking Thresholds

![](tweakthresholds.svg)
<!-- .element: class="stretch plain" -->
---
<!-- .element: class="titleslide"  data-background="../_chapterimg/17_fairnessgame.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Building Fair Products



----
## Learning Goals

* Understand the role of requirements engineering in selecting ML
fairness criteria
* Understand the process of constructing datasets for fairness
* Document models and datasets to communicate fairness concerns
* Consider the potential impact of feedback loops on AI-based systems
  and need for continuous monitoring
* Consider achieving fairness in AI-based systems as an activity throughout the entire development cycle

----
## Most Fairness Discussions are Model-Centric or Pipeline-Centric

![](fairness-lifecycle.jpg)
<!-- .element: class="stretch" -->

<!-- references_ -->

_Fairness-aware Machine Learning_, Bennett et al., WSDM Tutorial (2019).


----
## Fairness Problems are System-Wide Challenges

* **Requirements engineering challenges:** How to identify fairness concerns, fairness metric, design data collection and labeling
* **Human-computer-interaction design challenges:** How to present results to users, fairly collect data from users, design mitigations
* **Quality assurance challenges:** Evaluate the entire system for fairness, continuously assure in production
* **Process integration challenges:** Incoprorate fairness work in development process
* **Education and documentation challenges:** Create awareness, foster interdisciplinary collaboration


----
## Negotiate Fairness Goals/Measures

Equality or equity? Equalized odds? ...

Cannot satisfy all. People have conflicting preferences...

> *Treating everybody equally in a meritocracy will reinforce existing inequalities whereas uplifting disadvantaged communities can be seen as giving unfair advantages to people who contributed less, making it harder to succeed in the advantaged group merely due to group status.*



----
## Making Rare Skills Attainable


![radiology](radiology.jpg)

> We should stop training radiologists now. It’s just completely obvious that within five years, deep learning is going to do better than radiologists. -- [Geoffrey Hinton](https://www.youtube.com/watch?v=2HMPRXstSvQ&t=29s), 2016

----
[![Headline Rutkowski not happy about AI art](rutkowski.png)](https://www.technologyreview.com/2022/09/16/1059598/this-artist-is-dominating-ai-generated-art-and-hes-not-happy-about-it/)
<!-- .element: class="stretch" -->

----
## Who does the Fairness Work?

Within organizations usually little institutional support for fairness work, few activists

Fairness issues often raised by communities affected, after harm occurred

Affected groups may need to organize to affect change



*Do we place the cost of unfair systems on those already marginalized and disadvantaged?*



----
## Breakout: College Admission

![](college-admission.jpg)
<!-- .element: class="stretch" -->

Assume most universities want to automate admissions decisions. 


As a group in `#lecture`, tagging group members:

> What good or bad societal implications can you anticipate, beyond a single product? 
> Should we do something about it?










----
## 1. Avoid Unnecessary Distinctions


![Healthcare worker applying blood pressure monitor](blood-pressure-monitor.jpg)
<!-- .element: class="stretch" -->

"Doctor/nurse applying blood pressure monitor" -> "Healthcare worker applying blood pressure monitor"


----
## 2. Suppress Potentially Problem Outputs

![Twitter post of user complaining about misclassification of friends as Gorilla](apes.png)
<!-- .element: class="stretch" -->

*How to fix?*


----
## 4. Keep Humans in the Loop


![Temi.com screenshot](temi.png)
<!-- .element: class="stretch" -->

TV subtitles: Humans check transcripts, especially with heavy dialects


----
## Fairer Data Collection


Carefully review data collection procedures, sampling biases, what data is collected, how trustworthy labels are, etc.

Can address most sources of bias: tainted labels, skewed samples, limited features, sample size disparity, proxies:
* deliberate what data to collect
* collect more data, oversample where needed
* extra effort in unbiased labels

-> Requirements engineering, system engineering

-> World vs machine, data quality, data cascades


----
## Feedback Loops

![Feedback loop](feedbackloop.svg)
<!-- .element: class="plain" -->


----
## Barriers to Fairness Work

1. Rarely an organizational priority, mostly reactive (media pressure, regulators)
  * Limited resources for proactive work
  * Fairness work rarely required as deliverable, low priority, ignorable
  * No accountability for actually completing fairness work, unclear responsibilities


*What to do?*

----
## Affect Culture Change

Buy-in from management is crucial

Show that fairness work is taken seriously through action (funding, hiring, audits, policies), not just lofty mission statements

Reported success strategies:
1. Frame fairness work as financial profitable, avoiding rework and reputation cost
2. Demonstrate concrete, quantified evidence of benefits of fairness work
3. Continuous internal activism and education initiatives
4. External pressure from customers and regulators


----
## Documenting Model Fairness

Recall: Model cards

![Model Card Example](modelcards.png)
<!-- .element: class="stretch" -->

<!-- references_ -->

Mitchell, Margaret, et al. "[Model cards for model reporting](https://www.seas.upenn.edu/~cis399/files/lecture/l22/reading2.pdf)." In Proc. FAccT, 220-229. 2019.

----
## Documenting Fairness of Datasets

![Datasheet describing labeling procedure](datasheet2.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
*Excerpt from a “Data Card” for Google’s* [*Open Images Extended*](https://storage.googleapis.com/openimages/web/extended.html#miap) *dataset ([*full data card*](https://storage.googleapis.com/openimages/open_images_extended_miap/Open%20Images%20Extended%20-%20MIAP%20-%20Data%20Card.pdf)*) 

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/18_explainability.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Explainability and Interpretability


----
## Explainability as Building Block in Responsible Engineering

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->


----
# Learning Goals

* Understand the importance of and use cases for interpretability
* Explain the tradeoffs between inherently interpretable models and post-hoc explanations
* Measure interpretability of a model
* Select and apply techniques to debug/provide explanations for data, models and model predictions
* Eventuate when to use interpretable models rather than ex-post explanations


----

![Adversarial examples](adversarialexample.png)<!-- .element style="width:850px" -->

<!-- references -->

Image: Gong, Yuan, and Christian Poellabauer. "[An overview of vulnerabilities of voice controlled systems](https://arxiv.org/pdf/1803.09156.pdf)." arXiv preprint arXiv:1803.09156 (2018).

----
## Detecting Anomalous Commits

[![Reported commit](nodejs-unusual-commit.png)](nodejs-unusual-commit.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Goyal, Raman, Gabriel Ferreira, Christian Kästner, and James Herbsleb. "[Identifying unusual commits on GitHub](https://www.cs.cmu.edu/~ckaestne/pdf/jsep17.pdf)." Journal of Software: Evolution and Process 30, no. 1 (2018): e1893.

----
## Is this recidivism model fair?

```fortran
IF age between 18–20 and sex is male THEN 
  predict arrest
ELSE IF age between 21–23 and 2–3 prior offenses THEN 
  predict arrest
ELSE IF more than three priors THEN 
  predict arrest
ELSE 
  predict no arrest
```

<!-- references -->

Rudin, Cynthia. "[Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead](https://arxiv.org/abs/1811.10154)." Nature Machine Intelligence 1, no. 5 (2019): 206-215.  

----
## How to interpret the results?

![Screenshot of the COMPAS tool](compas_screenshot.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Image source (CC BY-NC-ND 4.0): Christin, Angèle. (2017). Algorithms in practice: Comparing web journalism and criminal justice. Big Data & Society. 4. 

----
![News headline: Stanford algorithm for vaccine priority controversy](stanford.png)
<!-- .element: class="stretch" -->


----
## Debugging

<!-- colstart -->

* Why did the system make a wrong prediction in this case?
* What does it actually learn?
* What data makes it better?
* How reliable/robust is it?
* How much does second model rely on outputs of first?
* Understanding edge cases

<!-- col -->

![Turtle recognized as gun](gun.png)

<!-- colend -->

**Debugging is the most common use in practice** (Bhatt et al. "Explainable machine learning in deployment." In Proc. FAccT. 2020.)



----
# Understanding a Model

Levels of explanations:

* **Understanding a model**
* Explaining a prediction
* Understanding the data

----
## Inherently Interpretable: Sparse Linear Models

$f(x) = \alpha + \beta_1 x_1 + ... + \beta_n x_n$

Truthful explanations, easy to understand for humans

Easy to derive contrastive explanation and feature importance

Requires feature selection/regularization to minimize to few important features (e.g. Lasso); possibly restricting possible parameter values

----
## Score card: Sparse linear model with "round" coefficients

![Scoring card](scoring.png)
<!-- .element: class="stretch" -->
 


----
## Post-Hoc Model Explanation: Global Surrogates

1. Select dataset X (previous training set or new dataset from same distribution)
2. Collect model predictions for every value: $y_i=f(x_i)$
3. Train *inherently interpretable* model $g$ on (X,Y)
4. Interpret surrogate model $g$


Can measure how well $g$ fits $f$ with common model quality measures, typically $R^2$

**Advantages? Disadvantages?**

Notes:
Flexible, intuitive, easy approach, easy to compare quality of surrogate model with validation data ($R^2$).
But: Insights not based on real model; unclear how well a good surrogate model needs to fit the original model; surrogate may not be equally good for all subsets of the data; illusion of interpretability.
Why not use surrogate model to begin with?


----
## Post-Hoc Model Explanation: Feature Importance


![FI example](featureimportance.png)
<!-- .element: class="stretch" -->

<!-- reference_ -->

Source: 
Christoph Molnar. "[Interpretable Machine Learning](https://christophm.github.io/interpretable-ml-book/)." 2019

----
## Post-Hoc Model Explanation: Partial Dependence Plot (PDP)


![PDP Example](pdp.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Source: 
Christoph Molnar. "[Interpretable Machine Learning](https://christophm.github.io/interpretable-ml-book/)." 2019

Note: bike rental data in DC



----
## Understanding Predictions from Inherently Interpretable Models is easy

Derive key influence factors or decisions from model parameters

Derive contrastive counterfacturals from models

**Examples:** Predict arrest for 18 year old male with 1 prior:

```fortran
IF age between 18–20 and sex is male THEN predict arrest
ELSE IF age between 21–23 and 2–3 prior offenses THEN predict arrest
ELSE IF more than three priors THEN predict arrest
ELSE predict no arrest
```


----
## Posthoc Prediction Explanation: Feature Influences

*Which features were most influential for a specific prediction?*


![Lime Example](lime2.png)
<!-- .element: class="stretch" -->


<!-- references_ -->
Source: https://github.com/marcotcr/lime 

----
## Feature Influences in Images

![Lime Example](lime_cat.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Source: https://github.com/marcotcr/lime 



----
## Example: Anchors

![Example](anchors-example3.png)


<!-- references -->
Source: Ribeiro, Marco Tulio, Sameer Singh, and Carlos Guestrin. "[Anchors: High-precision model-agnostic explanations](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/download/16982/15850)." In Thirty-Second AAAI Conference on Artificial Intelligence. 2018.






----
## Multiple Counterfactuals

<div class="smallish">

<!-- colstart -->

Often long or multiple explanations

> Your loan application has been *declined*. If your *savings account* ...

> Your loan application has been *declined*. If your lived in ...

Report all or select "best" (e.g. shortest, most actionable, likely values)

<!-- col -->
*(Rashomon effect)*

![Rashomon](rashomon.jpg)


<!-- colend -->

</div>


----
![Adversarial examples](adversarialexample.png)<!-- .element style="width:1000px" -->



----
## Prototypes and Criticisms

* *Prototype* is a data instance that is representative of all the data
* *Criticism* is a data instance  not well represented by the prototypes

![Example](prototype-dogs.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Source: 
Christoph Molnar. "[Interpretable Machine Learning](https://christophm.github.io/interpretable-ml-book/)." 2019

----
## Influential Instance

**Data debugging:** *What data most influenced the training?*

![Example](influentialinstance.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Source: 
Christoph Molnar. "[Interpretable Machine Learning](https://christophm.github.io/interpretable-ml-book/)." 2019




----
## Breakout: Debugging with Explanations

<div class="smallish">

In groups, discuss which explainability approaches may help and why. Tagging group members, write to `#lecture`.

<!-- colstart -->
*Algorithm bad at recognizing some signs in some conditions:*
![Stop Sign with Bounding Box](stopsign.jpg)
<!-- col -->
*Graduate appl. system seems to rank applicants from HBCUs low:*
![Cheyney University founded in 1837 is the oldest HBCU](cheyneylibrary.jpeg)
<!-- colend -->

</div>

<!-- references -->
Left Image: CC BY-SA 4.0, Adrian Rosebrock 







----
<!-- colstart -->
![Positive example](https://pair.withgoogle.com/assets/ET1_aim-for.png)<!-- .element: style="width:300px" -->


<!-- col -->
![Negative example](https://pair.withgoogle.com/assets/ET1_avoid.png)<!-- .element: style="width:300px" -->
<!-- col -->



Tell the user when a lack of data might mean they’ll need to use their own judgment. Don’t be afraid to admit when a lack of data could affect the quality of the AI recommendations.

<!-- colend -->

<!-- references -->
Source:
[People + AI Guidebook](https://pair.withgoogle.com/research/), Google

----
## Setting Cancer Imaging -- What explanations do radiologists want?

![](cancerpred.png)

* *Past attempts often not successful at bringing tools into production. Radiologists do not trust them. Why?*
* [Wizard of oz study](https://en.wikipedia.org/wiki/Wizard_of_Oz_experiment) to elicit requirements

----
## Explanations foster Trust

Users are less likely to question the model when explanations provided
* Even if explanations are unreliable
* Even if explanations are nonsensical/incomprehensible

**Danger of overtrust and intentional manipulation**

<!-- references -->
Stumpf, Simone, Adrian Bussone, and Dympna O’sullivan. "Explanations considered harmful? user interactions with machine learning systems." In Proceedings of the ACM SIGCHI Conference on Human Factors in Computing Systems (CHI). 2016.

----
![3 Conditions of the experiment with different explanation designs](explanationexperimentgame.png)

(a) Rationale, (b) Stating the prediction, (c) Numerical internal values

Observation: Both experts and non-experts overtrust numerical explanations, even when inscrutable.

<!-- references -->
Ehsan, Upol, Samir Passi, Q. Vera Liao, Larry Chan, I. Lee, Michael Muller, and Mark O. Riedl. "The who in explainable AI: how AI background shapes perceptions of AI explanations." arXiv preprint arXiv:2107.13509 (2021).




----
## "Stop explaining ..."

<div class="smallish">

Hypotheses:
* It is a myth that there is necessarily a trade-off between accuracy and interpretability (when having meaningful features)
* Explainable ML methods provide explanations that are not faithful to what the original model computes
* Explanations often do not make sense, or do not provide enough detail to understand what the black box is doing
* Black box models are often not compatible with situations where information outside the database needs to be combined with a risk assessment
* Black box models with explanations can lead to an overly complicated decision pathway that is ripe for human error

</div>

<!-- references -->

Rudin, Cynthia. "Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead." Nature Machine Intelligence 1.5 (2019): 206-215. ([Preprint](https://arxiv.org/abs/1811.10154))

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/19_accountability.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Transparency and Accountability

<!-- image: https://commons.wikimedia.org/wiki/File:Kerlikowske_testifies_before_Senate_Finance_Committee_(26349370364).jpg -->

----
## More Explainability, Policy, and Politics

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->



----
# Learning Goals

* Explain key concepts of transparency and trust
* Discuss whether and when transparency can be abused to game the system
* Design a system to include human oversight
* Understand common concepts and discussions of accountability/culpability 
* Critique regulation and self-regulation approaches in ethical machine learning



----
## Case Study: Facebook's Feed Curation

![Facebook with and without filtering](facebook.png)
<!-- .element: class="stretch" -->


<!-- references_ -->

Eslami, Motahhare, et al. [I always assumed that I wasn't really that close to [her]: Reasoning about Invisible Algorithms in News Feeds](http://eslamim2.web.engr.illinois.edu/publications/Eslami_Algorithms_CHI15.pdf). In Proc. CHI, 2015.






----
# Gaming/Attacking the Model with Explanations?

*Does providing an explanation allow customers to 'hack' the system?*

* Loan applications?
* Apple FaceID?
* Recidivism?
* Auto grading?
* Cancer diagnosis?
* Spam detection?


----
## Human Oversight and Appeals

* Unavoidable that ML models will make mistakes
* Users knowing about the model may not be comforting 
* Inability to appeal a decision can be deeply frustrating

<div class="tweet" data-src="https://twitter.com/dhh/status/1192945019230945280"></div>


----
## Who is responsible?

![teen-suicide-rate](teen-suicide-rate.png)<!-- .element: style="width:950px" -->


----
## Easy to Blame "The Algorithm" / "The Data" / "Software"

> "Just a bug, things happen, nothing we could have done"
  
- But system was designed by humans
- But humans did not anticipate possible mistakes, did not design to mitigate mistakes
- But humans made decisions about what quality was good enough
- But humans designed/ignored the development process
- But humans gave/sold poor quality software to other humans
- But humans used the software without understanding it
- ...

----
![Stack overflow survey on responsible](stackoverflow.png)<!-- .element: style="width:1250px" -->

<!-- references -->
Results from the [2018 StackOverflow Survey](https://insights.stackoverflow.com/survey/2018/#technology-and-society)

----
![Self regulation of tech companies on facial recognition](npr_facialrecognition.png)


----
![Responsible AI website from Microsoft](responsibleai.png)


----
[![Forbes Article: This Is The Year Of AI Regulations](airegulation.png)](https://www.forbes.com/sites/cognitiveworld/2020/03/01/this-is-the-year-of-ai-regulations/#1ea2a84d7a81)



---
<!-- .element: class="titleslide"  data-background="../_chapterimg/20_provenance.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production


# Versioning, Provenance, and Reproducability

<!-- image: https://commons.wikimedia.org/wiki/File:Kerlikowske_testifies_before_Senate_Finance_Committee_(26349370364).jpg -->

----
## More Foundational Technology for Responsible Engineering

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->



----
# Learning Goals

* Judge the importance of data provenance, reproducibility and explainability for a given system
* Create documentation for data dependencies and provenance in a given system
* Propose versioning strategies for data and models
* Design and test systems for reproducibility

----
![Example of dataflows between 4 sources and 3 models in credit card application scenario](creditcard-provenance.svg)
<!-- .element: class="plain stretch" -->


----

## Breakout Discussion: Movie Predictions

<div class="smallish">

> Assume you are receiving complains that a child gets many recommendations about R-rated movies

In a group, discuss how you could address this in your own system and post to `#lecture`, tagging team members:

* How could you identify the problematic recommendation(s)?
* How could you identify the model that caused the prediction?
* How could you identify the training code and data that learned the model?
* How could you identify what training data or infrastructure code "caused" the recommendations?

</div>

<!-- references -->

K.G Orphanides. [Children's YouTube is still churning out blood, suicide and cannibalism](https://www.wired.co.uk/article/youtube-for-kids-videos-problems-algorithm-recommend). Wired UK, 2018; 
Kristie Bertucci. [16 NSFW Movies Streaming on Netflix](https://www.gadgetreview.com/16-nsfw-movies-streaming-on-netflix). Gadget Reviews, 2020


----

## Data Provenance

<!-- colstart -->
* Track origin of all data
    - Collected where?
    - Modified by whom, when, why?
    - Extracted from what other data or model or algorithm?
* ML models often based on data drived from many sources through many steps, including other models
<!-- col -->

![Example of dataflows between 4 sources and 3 models in credit card application scenario](creditcard-provenance.svg)
<!-- .element: class="plain stretch" -->

<!-- colend -->


----
## Versioning Strategies for Datasets

1. Store copies of entire datasets (like Git), identify by checksum
2. Store deltas between datasets (like Mercurial)
3. Offsets in append-only database (like Kafka), identify by offset
4. History of individual database records (e.g. S3 bucket versions)
    - some databases specifically track provenance (who has changed what entry when and how)
    - specialized data science tools eg [Hangar](https://github.com/tensorwerk/hangar-py) for tensor data
5. Version pipeline to recreate derived datasets ("views", different formats)
    - e.g. version data before or after cleaning?


----
## Aside: Git Internals

![Git internal model](https://git-scm.com/book/en/v2/images/data-model-4.png)<!-- .element: style="width:900px" -->

<!-- references -->

Scott Chacon and Ben Straub. [Pro Git](https://git-scm.com/book/en/v2/Git-Internals-Git-References). 2014


----
## Example: DVC

```sh
dvc add images
dvc run -d images -o model.p cnn.py
dvc remote add myrepo s3://mybucket
dvc push
```

* Tracks models and datasets, built on Git
* Splits learning into steps, incrementalization
* Orchestrates learning in cloud resources


https://dvc.org/



----
## ModelDB Example

```python
from verta import Client
client = Client("http://localhost:3000")

proj = client.set_project("My first ModelDB project")
expt = client.set_experiment("Default Experiment")

# log the first run
run = client.set_experiment_run("First Run")
run.log_hyperparameters({"regularization" : 0.5})
run.log_dataset_version("training_and_testing_data", dataset_version)
model1 = # ... model training code goes here
run.log_metric('accuracy', accuracy(model1, validationData))
run.log_model(model1)

# log the second run
run = client.set_experiment_run("Second Run")
run.log_hyperparameters({"regularization" : 0.8})
run.log_dataset_version("training_and_testing_data", dataset_version)
model2 = # ... model training code goes here
run.log_metric('accuracy', accuracy(model2, validationData))
run.log_model(model2)
```


----

## Logging and Audit Traces


**Key goal:** If a customer complains about an interaction, can we reproduce the prediction with the right model? Can we debug the model's pipeline and data? Can we reproduce the model?

* Version everything
* Record every model evaluation with model version
* Append only, backed up



```
<date>,<model>,<model version>,<feature inputs>,<output>
<date>,<model>,<model version>,<feature inputs>,<output>
<date>,<model>,<model version>,<feature inputs>,<output>
```


---
<!-- .element: class="titleslide"  data-background="../_chapterimg/21_security.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Security and Privacy




<!-- img: https://pixabay.com/photos/castles-padlocks-love-lock-love-505878/ -->


----
## More responsible engineering...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->


----
## Learning Goals

* Explain key concerns in security (in general and with regard to ML models)
* Identify security requirements with threat modeling
* Analyze a system with regard to attacker goals, attack surface, attacker capabilities 
* Describe common attacks against ML models, including poisoning and evasion attacks
* Understand design opportunities to address security threats at the system level
* Apply key design principles for secure system design


----
## Evasion Attacks (Adversarial Examples)

![](evasion-attack.png)
<!-- .element: class="stretch" -->

Attack at inference time
* Add noise to an existing sample & cause misclassification
* Possible with and without access to model internals

<!-- references_ -->
_Accessorize to a Crime: Real and Stealthy Attacks on State-of-the-Art
Face Recognition_, Sharif et al. (2016).

----
## Task Decision Boundary vs Model Boundary

[![Decision boundary vs model boundary](decisionboundary.png)](decisionboundary.png)


<!-- references -->
From Goodfellow et al (2018). [Making machine learning robust against adversarial inputs](https://par.nsf.gov/servlets/purl/10111674). *Communications of the ACM*, *61*(7), 56-66. 

Note:
Exploiting inaccurate model boundary and shortcuts

* Decision boundary: Ground truth; often unknown and not specifiable
* Model boundary: What is learned; an _approximation_ of
decision boundary



----
## Untargeted Poisoning Attack on Availability

<!-- colstart -->

Inject mislabeled training data to damage model quality
  * 3% poisoning => 11% decrease in accuracy (Steinhardt, 2017)

Attacker must have some access to the public or private training set

<!-- col -->

*Example: Anti-virus (AV) scanner: AV company (allegedly) poisoned competitor's model by submitting fake viruses*

![](virus.png)


<!-- colend -->
  

----
## Targeted Poisoning Attacks on Integrity

Insert training data with seemingly correct labels

![](spam.jpg)
<!-- .element: class="stretch" -->

More targeted than availability attack, cause specific misclassification

<!-- references_ -->
_Poison Frogs! Targeted Clean-Label Poisoning Attacks on Neural
Networks_, Shafahi et al. (2018)


----
## Model Stealing Attacks

![Bing stealing search results from Google](bing.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Singel. [Google Catches Bing Copying; Microsoft Says 'So What?'](https://www.wired.com/2011/02/bing-copies-google/). Wired 2011.

----
## Model Inversion against Confidentiality

<!-- colstart -->

Given a model output (e.g., name of a person), infer the
corresponding, potentially sensitive input (facial image of the
person)
* e.g., gradient descent on input space 

<!-- col -->


![](model-inversion-image.png)

<!-- colend -->


<!-- references -->
_Model Inversion Attacks that Exploit Confidence Information and Basic
Countermeasures_, M. Fredrikson et al. in CCS (2015).


----
## Breakout: Dashcam System

<!-- colstart -->

Recall: Dashcam system from I2/I3

As a group, tagging members, post in `#lecture`:
  * Security requirements
  * Possible (ML) attacks on the system
  * Possible mitigations against these attacks

<!-- col -->

![](dashcam-architecture.jpg)

<!-- colend -->


----
## State of ML Security

![](arms-race.jpg)<!-- .element: style="width:1200px" -->



----
## STRIDE Threat Modeling

![](stride.png)
<!-- .element: class="stretch" -->

A systematic approach to identifying threats (i.e., attacker actions)
* Construct an architectural diagram with components & connections
* Designate the trust boundary 
* For each untrusted component/connection, identify threats
* For each potential threat, devise a mitigation strategy

<!-- references_ -->

[More info: STRIDE approach](https://docs.microsoft.com/en-us/archive/msdn-magazine/2006/november/uncover-security-design-flaws-using-the-stride-approach)

----
## Secure Design Principles

*Minimize the impact of a compromised component*
 * **Principle of least privilege:** A component given only minimal privileges needed to fulfill its functionality
 * **Isolation/compartmentalization:** Components should be able to interact with each other no more than necessary
 * **Zero-trust infrastructure:** Components treat inputs from each other as potentially
  malicious

*Monitoring & detection*
* Identify data drift and unusual activity

----
[![Article: 30 COMPANIES MERGING AI AND CYBERSECURITY TO KEEP US SAFE AND SOUND](30aisec.png)](https://builtin.com/artificial-intelligence/artificial-intelligence-cybersecurity)
<!-- .element: class="stretch" -->


----

![Target headline](target-headline.png)
<!-- .element: class="stretch" -->

> Andew Pole, who heads a 60-person team at Target that studies
customer behavior, boasted at a conference in 2010 about a proprietary
program that could identify women - based on their purchases and
demographic profile - who were pregnant.

<!-- references_ -->
Lipka. "[What Target knows about you](https://www.reuters.com/article/us-target-breach-datamining/what-target-knows-about-you-idUSBREA0M1JM20140123)". Reuters, 2014

----
## Data Lakes

![data lakes](data-lake.png)
<!-- .element: class="stretch" -->

*Who has access?*

----
## Privacy Consent and Control

![Techcrunch privacy](techcrunch-privacy.png)
<!-- .element: class="stretch" -->
---
<!-- .element: class="titleslide"  data-background="../_chapterimg/22_safety.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Safety




<!-- img: https://pixabay.com/photos/circus-the-fire-breathing-fire-4318438/ -->

----
## Mitigating more mistakes...

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->




----
## Learning Goals

* Understand safety concerns in traditional and AI-enabled systems
* Apply hazard analysis to identify risks and requirements and understand their limitations
* Discuss ways to design systems to be safe against potential failures 
* Suggest safety assurance strategies for a specific project
* Describe the typical processes for safety evaluations and their limitations





----
# AI Safety

![Robot uprising](robot-uprising.jpg)
 
<!-- references -->
Amodei, Dario, Chris Olah, Jacob Steinhardt, Paul Christiano, John Schulman, and Dan Mané. "[Concrete problems in AI safety](https://arxiv.org/pdf/1606.06565.pdf%20http://arxiv.org/abs/1606.06565)." arXiv preprint arXiv:1606.06565 (2016).

----
## Reward Hacking -- Many Examples

<div class="tweet" data-src="https://twitter.com/vkrakovna/status/980786258883612672"></div>


----
## Practical Alignment Problems

Does the model goal align with the system goal? Does the system goal align with the user's goals?
* Profits (max. accuracy) vs fairness
* Engagement (ad sales) vs enjoyment, mental health
* Accuracy vs operating costs

Test model *and* system quality *in production*

(see requirements engineering and architecture lectures)



    
----
## Robustness in a Safety Setting

* Does the model reliably detect stop signs?
* Also in poor lighting? In fog? With a tilted camera? Sensor noise?
* With stickers taped to the sign? (adversarial attacks)

![Stop Sign](stop-sign.png)
<!-- .element: class="stretch" -->

<!-- references_ -->
Image: David Silver. [Adversarial Traffic Signs](https://medium.com/self-driving-cars/adversarial-traffic-signs-fd16b7171906). Blog post, 2017

----
## No Model is Fully Robust

* Every useful model has at least one decision boundary
* Predictions near that boundary are not (and should not) be robust

![Decision boundary](decisionboundary2.svg)
<!-- .element: class="stretch" -->

----
## Breakout: Robustness

Scenario: Medical use of transcription service, dictate diagnoses and prescriptions

As a group, tagging members, post to `#lecture`:

> 1. What safety concerns can you anticipate?
> 2. What notion of robustness are you concerned about (i.e., what distance function)?
> 3. How could you use robustness to improve the product (i.e., when/how to check robustness)?






----
## Safety != Reliability

Reliability = absence of defects, mean time between failure

Safety = prevents accidents, harms

Can build safe systems from unreliable components (e.g. redundancy, safeguards)

System may be unsafe despite reliable components (e.g. stronger gas tank causes more severe damage in incident)


Accuracy and robustness are about reliability!


----
## Safety of AI-Enabled Systems

<div class="tweet" data-src="https://twitter.com/EmilyEAckerman/status/1186363305851576321"></div>

----
## Improving Safety of ML-Enabled Systems

Anticipate problems (hazard analysis, FTA, FMEA, HAZOP, ...)

Anticipate the existence of unanticipated problems

Plan for mistakes, design mitigations
* Human in the loop
* Undoable actions, failsoft
* Guardrails
* Mistaked detection
* Redundancy, ...

Improve reliability (accuracy, robustness)

----
## Demonstrating Safety

Two main strategies:

1. **Evidence of safe behavior in the field** 
   * Extensive field trials
   * Usually expensive
2. **Evidence of responsible (safety) engineering process**
   * Process with hazard analysis, testing mitigations, etc
   * Not sufficient to assure safety

Most standards require both



----
## Documenting Safety with Assurance (Safety) Cases

![](safetycase.svg)
<!-- .element: class="stretch plain " -->
--- 
<!-- .element: class="titleslide"  data-background="../_chapterimg/23_teams.jpg" -->
<div class="stretch"></div>

## Machine Learning in Production

# Fostering Interdisciplinary Teams

(Process and Team Reflections)




----
## One last crosscutting topic

![Overview of course content](../_assets/overview.svg)
<!-- .element: class="plain stretch" -->




----

## Learning Goals

* Understand different roles in projects for AI-enabled systems
* Plan development activities in an inclusive fashion for participants in different roles
* Diagnose and address common teamwork issues
* Describe agile techniques to address common process and communication issues


----
# Case Study: Depression Prognosis on Social Media

![TikTok logo](tiktok.jpg)


----
## Continuum of Skills

* Software Engineer
* Data Engineer
* Data Scientist
* Applied Scientist
* Research Scientist


<!-- references -->
Talk: Ryan Orban. [Bridging the Gap Between Data Science & Engineer: Building High-Performance Teams](https://www.slideshare.net/ryanorban/bridging-the-gap-between-data-science-engineer-building-highperformance-teams/3-Software_Engineer_Data_Engineer_Data). 2016

----
## Process Costs

![](connectedteams.svg)
<!-- .element: class="stretch plain" -->

*n(n − 1) / 2* communication links within a team

----
## Congurence

![](congruence.svg)
<!-- .element: class="plain stretch" -->

Structural congruence,
Geographical congruence,
Task congruence,
IRC communication congruence



----
## Breakout: Team Structure for Depression Prognosis

In groups, tagging team members, discuss and post in `#lecture`:
* How to decompose the work into teams?
* What roles to recruit for the teams

![TikTok logo](tiktok.jpg)


----
![Team collaboration within a large tech company](team-collaboration1.png)
<!-- .element: class="stretch plain" -->

----
![Team collaboration within a large tech company](team-collaboration2.png)
<!-- .element: class="stretch plain" -->


----
## Conflicting Goals?

![DevOps](devops.png)<!-- .element: style="width:1000px" -->




----
## Matrix Organization

![](matrix-only.svg)
<!-- .element: class="stretch plain" -->

----
## Project Organization

![](project-only.svg)
<!-- .element: class="stretch plain" -->

----
# Team issues: Groupthink

![](groupthink.png)

----
![](svposter.png)<!-- .element: style="width:950px" -->

----
## Mitigation Strategies

* Diversity in team composition
* Culture of open conflicts
* Appoint devil's advocate in discussions, moderate and rotate speaker order, leaders hide opinions in discussions
* Involve outside experts
* Always request a second solution
* Monitoring and process measurement
* Agile techniques as planning poker, on-site customer


----
# Learning from DevOps

![DevOps](devops.png)<!-- .element: class="stretch plain" style="width:900px" -->



---
# Today

<!-- colstart -->
(1)

**Looking back at the semester**

(413 slides in 40 min)

<!-- col -->
(2)

**Discussion of future of ML in Production**

<!-- col -->
(3)

**Feedback for future semesters**

<!-- colend -->




---
<!-- .element: class="titleslide"  data-background="../_chapterimg/24_future.jpg" -->
<div class="stretch"></div>



# The Future of Machine Learning in Production?

(closing remarks)




----
## Are Software Engineers Disappearing?


<div class="tweet" data-src="https://twitter.com/karpathy/status/893576281375219712"></div>


<!-- references -->
see also Andrej Karpathy. [Software 2.0](https://medium.com/@karpathy/software-2-0-a64152b37c35). Blog, 2017



Note: Andrej Karpathy is the director of AI at Tesla and coined the term Software 2.0


----
## Are Data Scientists Disappearing?

[![Forbes Article: AutoML 2.0: Is The Data Scientist Obsolete?](automl.png)](https://www.forbes.com/sites/cognitiveworld/2020/04/07/automl-20-is-the-data-scientist-obsolete/#28f4a5b053c9)

<!-- references -->
Ryohei Fujimaki. [AutoML 2.0: Is The Data Scientist Obsolete?](https://www.forbes.com/sites/cognitiveworld/2020/04/07/automl-20-is-the-data-scientist-obsolete/#28f4a5b053c9) Forbes, 2020

----
## Are Data Scientists Disappearing?

> However, AutoML does not spell the end of data scientists, as it doesn’t “AutoSelect” a business problem to solve, it doesn’t AutoSelect indicative data, it doesn’t AutoAlign stakeholders, it doesn’t provide AutoEthics in the face of potential bias, it doesn’t provide AutoIntegration with the rest of your product, and it doesn’t provide AutoMarketing after the fact. -- [Frederik Bussler](https://towardsdatascience.com/will-automl-be-the-end-of-data-scientists-9af3e63990e0)

<!-- references -->
Frederik Bussler. [Will AutoML Be the End of Data Scientists?](https://towardsdatascience.com/will-automl-be-the-end-of-data-scientists-9af3e63990e0), Blog 2020

----
## SE4AI Research: More SE Power to Data Scientists?

## SE4AI Research: More DS Power to Software Engineers?

<!-- discussion -->

----
![Tweet: "Virtually *everyone* is / will soon be building ML applications. Only few can afford dedicated software engineers to team up with, or SE education for themselves. It would be more inclusive to build SE into the ML processes more fundamentally, so that everyone could build better"](virtuallyeveryone.png)
<!-- .element: class="stretch" -->


----
![Unicorn](unicorn.jpg)
<!-- .element: class="stretch" -->

----
## Analogy

![Renovation](renovation.jpg)

----
## Analogy

<!-- colstart -->
![Hammer](hammer2.jpg)
<!-- col -->
![Nail gun](nailgun.jpg)
<!-- colend -->

*(better tools don't replace the knowledge to use them)*
----
## My View 

> This is an education problem, more than a research problem. 

> Interdisciplinary teams, mutual awareness and understanding

> Software engineers and data scientists will each play an essential role

----
## DevOps as a Role Model

![DevOps](devops.png)

Joint responsibilities, joint processes, joint tools, joint vocabulary


---
# One Last Time: Transcription

![](temi.png)


---
# Feedback

----
## Some things we tried

* Scaling the class!
* Stable TA-team mapping and checkins
* In-class interactions with 50+ students
* In-class breakouts, posting to slack
* Clear specifications for homework, pass/fail grading, allow resubmission
* Open-ended reading quizzes
* Credit for social activities in teams
* Team checkins, peer grading for "team citizenship"
* Slack for coordination and questions

----
## Feedback

* What was useful?
* What could be improved?
* Where did we overdo it with the homework?
* Ideas for better scaling?
* How to better support teamwork?
* How to better use the recitations?

<!-- discussion -->

---
<!-- .element: class="titleslide"  data-background="../_chapterimg/24_summary.jpg" -->
<div class="stretch"></div>

# Thank you!






