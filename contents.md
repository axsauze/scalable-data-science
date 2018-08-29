<!-- .slide: data-background="images/network-background.jpg" class="background" -->

<h2>Scalable Data Science</h2>
<h4>The state of machine learning operations in 2018</h4>
<p>
  <br />
  <br />
    Alejandro Saucedo <br/><br/>
    <a href="http://twitter.com/AxSaucedo">@AxSaucedo</a><br/>
    <a href="http://linkedin.com/in/AxSaucedo">in/axsaucedo</a><br/>
  <br />
</p>
<p>

[NEXT]
<!-- .slide: data-background="images/network-background.jpg" class="background" -->

<h2>Scalable Data Science</h2>
<h4>The state of machine learning operations in 2018</h4>

<table class="bio-table">
  <tr>
    <td style="float: left">
        ![portrait](images/alejandro.jpg)
        <br>
        <font style="font-weight: bold; color: white">Alejandro Saucedo</font>
        <br>
        <br>
    </td>
    <td style="float: left; color: white; font-size: 0.7em;">

        Head of Solutions Eng./Science
        <br>
        <a style="color: cyan" href="http://e-x.io">Eigen Technologies</a
        <br>
        <br>
        <br>
        Chairman
        <br>
        <a style="color: cyan" href="http://ethical.institute">The Institute for Ethical AI & ML</a>
        <br>
        <br>
        Member, Broader AI Expert Group
        <br>
        <a style="color: cyan" href="#">European Commission</a>
        <br>
        <br>
        Advisory group
        <br>
        <a style="color: cyan" href="http://teensinai.com">TeensInAI</a>
        <br>

    </td>
  </tr>
  <tr>
  </tr>
</table>
  

[NEXT]
<!-- .slide: data-background="images/network-background.jpg" class="background smallquote" -->

# Eigen Technologies

> Building front-/back-office automation ML
> <br>
> <br>
> Working in Finance, Legal and Insurance
>
> Recently raised 17.5m to expand operations
>
> Using probabilistic models for text analysis

### PS. We are hiring -> <a href="http://eigentech.com">eigentech.com</a>

    
[NEXT]
<!-- .slide: data-background="images/network-background.jpg" class="background smallquote" -->

## Scaling Data Science with MLOps

> Motivations & challenges
> <br>
> <br>
> Concepts & Best Practices
>
> Frameworks & libraries
>
> Closing words
>

####  Slides at: <a style="color: cyan" href="#">bit.ly/awesome-mlops</a>

[NEXT]
## #LetsDoThis

[NEXT SECTION]
# 1. Motivations & Challenges

[NEXT]
Data science generalised in two workflows

* Model Development
* Model Serving

![classification_large](images/mltemp1.png)

[NEXT]

If we have a small team of data scientists...
## We face a smaller number of issues

[NEXT]

* Small number of models to maintain
* Data scientists have knowledge of models in their head
* They each have their methods for tracking their progress
    * Some use Jupyter Notebooks
    * Some just put the data in different folders

<br>
### It all works relatively well!


[NEXT]

# However
As our data science requirements grow...
## We face new issues

[NEXT]

#### Large number of models developed and deployed

<div class="left-col">
![classification_large](images/mlmodles.png)
</div>
<div class="right-col">
    <ul>
        <li>Keep track of what version exists in each environment</li>
        <li>Deploying new models gets increasingly complex</li>
        <li>There might be disruption or downtime that may not be tolerable</li>
    </ul>
</div>

[NEXT]
#### Complexity increases orchestrating data flow

<div class="left-col">
    <ul>
        <li>Increasing number of pre/post processing jobs</li>
        <li>Data ingestion workflows growing complex</li>
        <li>Tracking what is running where is harder</li>
    </ul>
</div>
<div class="right-col">
![classification_large](images/crontab.jpg)
</div>

[NEXT]
#### When stuff goes wrong it's hard to trace back

<div class="left-col">
![classification_large](images/gitblame.jpg)
</div>

<div class="right-col">
    <ul>
        <li>Becomes a cat-and-mouse game</li>
        <li>Data scientists say it's a bug in the pipelines</li>
        <li>Data engineers say it's something wrong in the models</li>
    </ul>
</div>
[NEXT]
#### Each data scientist has their own set of tools

<div class="left-col">
    <ul>
        <li>Some ♥ R</li>
        <li>Some ♥ Python</li>
        <li>Some ♥ Spark</li>
    </ul>
</div>
<div class="right-col">
![classification_large](images/mlibs.jpg)
</div>

<br style="clear:both">
### Some ♥ all of them

[NEXT]

As we can see a lot of complexities arise...

[NEXT]

# Luckily for us
Many fellow colleagues have faced these issues for a while

Allowing us to gather a set of best practices

[NEXT SECTION]

# 2. ML-Ops Concepts 

[NEXT]

### As any technical function grows...

![classification_large](images/mltemp1.png)

[NEXT]

### So does their complexity

![classification_large](images/mlops1.png)

[NEXT]

### MLOps through 2 general principles

The data science operational layer focused on:

![classification_large](images/mlops2.png)

[NEXT]

Currently defining a new role within the data science teams

[NEXT]

#### Data Scientists 
In charge of development of models
<br>
<br>

#### Data Engineers 
In charge of development of data pipelines
<br>
<br>

### DevOps / DataOps / MLOps Engineers
In charge of productionisation of models, data pipelines & products

[NEXT]

Let's break down the two general principles

[NEXT]

## Point I - Model & Data Versioning

![classification_large](images/mltemp6.png)

The age-old question of reproducibility in data science

[NEXT]

This is a very interesting challenge

With a huge number of creative attempts

But all that agree on a set of core concepts

[NEXT]

### Dissecting each step in our pipelines

![classification_large](images/mltemp2.png)

Each stage has code/config, as well as specific data in/out 

[NEXT]

## Abstracting individual steps

<div style="float: left; width: 33%">
<h4>Data in </h4>

<pre><code class="code python hljs" style="font-size: 0.6em; line-height: 1em">
$ cat data-input.csv

>            Date    Open    High     Low   Close     Market Cap
> 1608 2013-04-28  135.30  135.98  132.10  134.21  1,500,520,000
> 1607 2013-04-29  134.44  147.49  134.00  144.54  1,491,160,000
> 1606 2013-04-30  144.00  146.93  134.05  139.00  1,597,780,000

</code></pre>
</div>

<div style="float: left; width: 33%">
<h4>Code / Config</h4>
<pre><code class="code python hljs" style="font-size: 0.6em; line-height: 1em">
$ cat feature-extractor.py

> def open_norm_feature_extractor(df):
>     feature = some_lib.get_open(df)
>     return feature


</code></pre>
</div>

<div style="float: left; width: 33%">
<h4>Data out</h4>
<pre><code class="code python hljs" style="font-size: 0.6em; line-height: 1em">
$ cat data-output.csv

>   Open 
>   0.57 
>   0.59 
>   0.47 


</code></pre>
</div>

If we can abstract and store these representations

We are able to recreate that step in isolation


[NEXT]

## Going one level higher

We can abstract our entire pipeline and data flows

![classification_large](images/mltemp5.png)

_note_
Similarly we can store the accuracy of the model
Together with all the parameters that were used to compute it

[NEXT]

This gets us closer to our ultimate objective:

# Reproducibility

[NEXT]

## Reproducibility is critical
#### It enables for:
* Traceablility when debugging for errors
* Transparency on the steps that lead to results
* Modularity of componets so they can be reused
* Abstraction to support multiple libraries 
* Robustness if we need to go back to a previous release

[NEXT]

Once we have our internal representations for our models...

### We are able to serve them in production

[NEXT]

### Point II - Model Deployment Orchestration

![classification_large](images/mltemp3.png)

Covers complexities of serving models in production

[NEXT]

#### Similar to CI / CD / Monitoring for software...

# But completely different

_note_
And it's different because we are not dealing with 
"just software"...

[NEXT]

### A. Karpathy on Software 2.0 (AKA ML)

1) We specify some goal on the behavior of a desirable program (instead of coding it)
```
(e.g., “satisfy a dataset of input-output pairs of examples,” 
or, “win a game of Go”)
```
2) write a rough skeleton of the code
```
(e.g., a neural net architecture) that identifies a 
subset of program space to search, 
```
3) use the computational resources at our disposal to search this space for a program that works.

[NEXT]

Let's see how this differs

[NEXT]

# Monitoring 

### Going beyond debug logs

[NEXT]

# Monitoring 

<div class="left-col">
<h3>Short term</h3>

<ul>
    <li>Anomalities </li>
    <li>Bias</li>
    <li>Comp. vs prev model</li>
</ul>
</div>

<div class="right-col">
<h3>Long term</h3>
<ul>
    <li>Errors</li>
    <li>Outages</li>
    <li>Performance</li>
</ul>
</div>

<br style="clear:both">
<br style="clear:both">
### Ensuring short and medium term approaches

[NEXT]

#### Quality control processes in production are 
## necessary 
#### and need to be specific to its usecase

[NEXT]

# Compliance 

### A boring word with exciting benefints

<div class="left-col">
<a href="https://www.youtube.com/watch?v=eOzl-LFqYFM" style="font-size: 0.6em">Guidelines for and properties of compliant ML</a>
![classification_large](images/compliant-ml.png)
<a href="https://www.youtube.com/watch?v=eOzl-LFqYFM" style="font-size: 0.6em">CNCF 2018 - Pachyderm</a>
</div>

<div class="right-col">
<br>

It's very important to know:
<ul>
    <li>What happened</li>
    <li>When it happened</li>
    <li>Why it happened</li>
    <li>How it happened</li>
</ul>
</div>

[NEXT]

This enables the data scientists, data engineers, and devops/mlops engineers to:
* Trace back issues
* Debug problems
* Report critical issues


[NEXT]

#### It's important to be prepared

<div class="left-col">
![classification_large](images/programming-gods.jpg)
</div>

<div class="right-col">

<br>
The production gods 
<br>
are not in our side


### We need to be 
### ready
</div>
<br style="clear: both">

And our deployment infrastructure should be as well

[NEXT]

# Resource allocation

With a compute-heavy ecosystem

And dynamic services that provide different functionality

We need to be able to allocate the right resources

[NEXT]

#### Resource allocation Makes a difference

![classification_large](images/arch3.png)

Compare traditional server allocation

[NEXT]

#### Resource allocation Makes a difference

![classification_large](images/arch2.png)

To auto-scale 

[NEXT]

#### Resource allocation Makes a difference

![classification_large](images/arch1.png)

To even serverless

[NEXT]

So now we understand some of the implications

## What's next?

### Let's have a look at some solutions

[NEXT SECTION]

# 3. ML-Ops ecosystem

[NEXT]

Let's have a look at what are some of the tools that are available

in the world of machine learning operations

and then let's then learn how these all fit together


[NEXT]

I'm putting together a list in Github on

# "Awesome MLOps"

with the tools available for ML Operations

## Feel free to chip in!

<br>
#### https://github.com/axsauze/awesome-machine-learning-operations

[NEXT]

# Part I 
## Model & Data Versioning Tools 

[NEXT]

## Data Version Control (DVC)

A full-on Open-source Version Control System for Data Science Projects

<div class="left-col">
<br>
A fork of git, built by iterative.ai, that allows for grouping data, 
config and code through a version control system
</div>

<div class="right-col">
![classification_large](images/dvc.png)
</div>

[NEXT]

## Data Version Control (DVC)

#### Add your data

```
dvc add images.zip
```

#### Connect data input, model output and code

```
dvc run -d images.zip -o model.p ./cnn.py
```

#### Add repository location (here is s3)

```
dvc remote add myrepo s3://mybucket
```

#### Push to the location specified

```
dvc push
```

[NEXT]

## ModelDB

A more implicit way of tracking the inputs, outputs and configurations on a library-level by extending the functions themselves. 

<div class="left-col">
<h4>Normal sklearn</h4>

<pre><code class="code python hljs" style="font-size: 1em; line-height: 1em">
def fit_and_predict(data):
    model.fit(data)
    preprocessor.transform(data)
    model.predict(data)

</code></pre>
</div>


<div class="right-col">
<h4>ModelDB-enabled</h4>

<pre><code class="code python hljs" style="font-size: 1em; line-height: 1em">
def fit_and_predict(data):
    model.fit_sync(data)
    preprocessor.transform_sync(data)
    model.predict_sync(data)

</code></pre>
</div>

This basically stores all the steps that were used, together with the results and predictions of the model


[NEXT]

## ModelDB

This allows for exploration of models that have been run

<iframe src="http://modeldb.csail.mit.edu:3000/projects/1/models" frameborder="0" style="width: 100%; height: 50vh"></iframe>

[NEXT]

## MLeap

Diving one level deeper into serialization of models

<div class="left-col">
![classification_large](images/mleapruntime.jpg)
</div>
<div class="right-col">
<br>
Standardisation of pipeline and model serialization for Spark, Tensorflow and sklearn built by Combust.ml
</div>

<br style="clear: both">
<br style="clear: both">
MLeap is used in open source projects that look to abstract the storage, deployment and execution of various machine learning libraries.


[NEXT]

## PMML

The Predictive Model Markup Language standard in XML

A standard way of representing machine learning model pipelines for storage

Several renowned systems actually use PMML to enable import/export of models across platforms

[NEXT]
## PMML

#### Exporting to PMML using sklearn2pmml
```
from sklearn import datasets, tree
iris = datasets.load_iris()
clf = tree.DecisionTreeClassifier()
clf = clf.fit(iris.data, iris.target)

from sklearn_pandas import DataFrameMapper
default_mapper = DataFrameMapper(
    [(i, None) for i in iris.feature_names + ['Species']])

from sklearn2pmml import sklearn2pmml
sklearn2pmml(estimator=clf,
             mapper=default_mapper,
             pmml="D:/workspace/IrisClassificationTree.pmml")
```

[NEXT]

## All-in-one Model Versioning 
# Pachyderm 

![classification_large](images/pachyderm.png)

Pachyderm is an end-to-end model-versioning framework that allows for high-level dynamic pipeline definitions.

[NEXT]

## Pachyderm

The Pachyderm frameowrk allows the users to define the data flows via JSON, and the framework takes care of data / code / configuration versioning 

_note_
# Part II 
## Model Deployment Orchestration

# Seldon Core





[NEXT SECTION]
<!-- .slide: data-background="images/network-background.jpg" class="background smallest" -->

## Scaling Data Science with MLOps

> Motivations & challenges
> <br>
> <br>
> Concepts & Best Practices
>
> Frameworks & libraries
>
> Closing words
>

####  Slides at: <a style="color: cyan" href="#">bit.ly/awesome-mlops</a>


[NEXT]
<!-- .slide: data-background="images/network-background.jpg" class="background" -->
### Scalable Data Science
https://github.com/axsauze/scalable-data-science

### Awesome MLOps
http://github.com/axsauze/awesome-machine-learning-operations

[NEXT]
<!-- .slide: data-background="images/network-background.jpg" class="background" -->

<h2>Scalable Data Science</h2>
<h4>The state of machine learning operations in 2018</h4>

<table class="bio-table">
  <tr>
    <td style="float: left">
        ![portrait](images/alejandro.jpg)
        <br>
        <font style="font-weight: bold; color: white">Alejandro Saucedo</font>
        <br>
        <br>
    </td>
    <td style="float: left; color: white; font-size: 0.7em;">

        Head of Solutions Eng./Science
        <br>
        <a style="color: cyan" href="http://e-x.io">Eigen Technologies</a
        <br>
        <br>
        <br>
        Chairman
        <br>
        <a style="color: cyan" href="http://ethical.institute">The Institute for Ethical AI & ML</a>
        <br>
        <br>
        Member, Broader AI Expert Group
        <br>
        <a style="color: cyan" href="#">European Commission</a>
        <br>
        <br>
        Advisory group
        <br>
        <a style="color: cyan" href="http://teensinai.com">TeensInAI</a>
        <br>

    </td>
  </tr>
  <tr>
  </tr>
</table>
  


