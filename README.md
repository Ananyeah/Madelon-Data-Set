# A Problem Statement for the Madelon Data Set 
## Steven Slezak
### 27 January 2018

### Introduction

The Center for Machine Learning and Intelligent Systems at the University of California, Irvine, maintains a web site containing over 400 data sets as a service to the machine learning community.  This site, [the UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/index.php), consists of data bases, domain theories, and data generators that are open source to any users.  This problem statement utilizes the *Madelon* [data set found there.](http://archive.ics.uci.edu/ml/datasets/madelon)

This problem statement includes the following:

1.  Domain: Artificial
2.  Problem Statement:  Classify Random Data (Training, Validating, Testing)
3.  Description of Data Set:  500 Features, Random, Dense, Bimodal
4.  Proposed Solution:  Kernel Methods and SVMs
5.  Benchmark Model:  Logistic Regression
6.  Performance Metrics:  BER and AUC
7.  Citations
8.  Jupyter Notebook with Associated Code


### Domain:  Artificial

The *Madelon* data set is an artificial data set developed for the 2003 NIPS feature selection challenge.  According to the NIPS 2003 workshop on feature extraction site, the *Madelon* data set was created with a particular purpose in mind, for "selecting a feature set when no feature is informative by itself."  *Madelon* was the only artificial data set in the 2003 NIPS challenge.  It was generated by the *hypercube_data.m* program.

The data set was never used before the 2003 NIPS challenge, though the idea for the program orginated with a study, "Grafting: Fast, Incremental Feature Selection by Gradient Descent in Function Space," Simon Perkins, Kevin Lacker, James Theiler; JMLR, 3(Mar):1333-1356, 2003. [http://www.jmlr.org/papers/volume3/perkins03a/perkins03a.pdf]

The technical memorandum for the *Madelon* data set, and others used in the 2003 NIPS challenge:  "Design of experiments for the NIPS 2003 variable selection benchmark," Isabelle Guyon; 2003.  [http://clopinet.com/isabelle/Projects/NIPS2003/Slides/NIPS2003-Datasets.pdf]

A summary of the main results from the 2003 NIPS challenge:  "Result Analysis of the NIPS 2003 Feature Selection Challenge," Isabelle Guyon, Steve Gunn, Asa Ben Hur, Gideon Dror; 2004. [http://clopinet.com/isabelle/Projects/NIPS2003/ggad-nips04.pdf]

### Problem Statement:  Feature Selection and Classify Random Data (Training, Validating, Testing)

According to the organizers of the 2003 NIPS challenge, in "Design for experiments" cited below, the "task of MADELON is to classify random data.  This is a two-class classification problem with sparse binary input variables."

If this sounds like an ambiguous problem, it turns out using randomly-generated artificial data arrayed in a five-dimensional space to predict random features is both ambiguous and difficult.  Statistical and machine learning methods can be used for feature selection and for classification.  The goal being to identify and select the random relevant features, as opposed to the far more numerous probes, and use them to predict the random labels for the data set, the integers *+1* and *-1*.  These are the two classes mentioned above.

The inputs are the randomly-generated integers arrayed in 500 columns.  The outputs will be predictions of the labels, *+1* and *-1*. 

The purpose will be to explore the cabilities of machine learning under ambiguous circumstances.  Ideally, the approach would be to tackle the problem by training different ML algorithms to fit the *Madelon* training data.  Model parameters would be adjusted in an effort to improve the fit to training data.  Once an acceptable fit was found, the "fitted" model would be run against the *Madelon* validation data for evaluation.  If these results are satisfactory, the model would be run against the *Madelon* test data set for a final fit and evaluation.

This procedure would be used for the different model candidates being evaluated. 

By using different types of classification models (for example, logistic regression, decision trees, random forests, naive Bayes, neural networks, kernels, etc.) within the framework of support vector machines, it might be possible to find an approach that results in improved performance over time.

For feature selection, the "Result Analysis" suggests the use a combination of "filters and embedded methods" for best results.  Random Forests can also be effective but only to generate features, not for purposes of classification.

The "Result Analysis" suggests two steps to take:

1.  reduce the number of features using "simple univariate significance tests" or by Principal Component Analysis
2.  apply a classification method based on "Bayesian neural network learning" with "computation by Markov chain Monte Carlo" simulation.

### Description of Data Set:  500 Features, Random, Dense, Bimodal

The *Madelon* data set consists of 500 features, randomly labelled as two classes, *+1* or *-1*.  The data are grouped into 32 clusters within a five-dimensional hypercube.  All data are integers.

The data sets consist of a training set, a validation set, and a test set.  Target values (*+1* and *-1*) exist only in the first two sets.  There are 2200 positive examples and 2200 negative examples.  There is also a label set, consisting of the labels *+1* and *-1*.

The distribution of the examples is illustrated below:

| **Set** | **Positive Examples** | **Negative Examples** | **Total** |
| :---: | :---: | :---: | :---: |
| Training Set | 1000 (45%) | 1000 (45%) | 2000 | 
| Validation Set | 300 (14%) | 300 (14%) | 600 |
| Test Set | 900 (41%) | 900 (41%) | 1800 | 
| Total | 2200 | 2200 | 4400 |

Information on the data sets, their dimensions, and memory usage follow:

| **Set** | **Dimensions** | **Memory (in MB)** |
| :---: | :---: | :---: |
| Training Set | 2000 x 500 | 4.05 |
| Validation Set | 599 x 500 | 1.25 |
| Test Set | 1800 x 500 | 3.65 | 
| Labels | 2000 x 1 | 0.0087 |

Total observations in the *Madelon* data set are over 2.2 million.

Of the 500 features, only 20 are considered relevant, or real variables.  The remaining 480 are "probes," distractor features with no predictive power.  These probes resemble relevant data but they carry no useful information.  They exist to introduce noise to the data.  The data set is considered dense, that is all rows are populated and no values are missing.  It is a multivariate data set with a bimodal distribution.

The 20 real features consist of five informative features and 15 linear combinations of the five informative features.  The five dimensions of the hypercube are the informative features.  The 15 linear combinations are redundant informative features.  These linear combinations also contribute to noise in the data set.  The order of the features was completely randomized.

### Proposed Solution: Kernel Methods and SVMs

Again, according to the organizers of the 2003 NIPS challenge, in "Result Analysis" below, kernel methods "are most popular" for approaching the classification problem, and most kernel methods were SVMs.  For *Madelon* specifically, "all best ranking groups used a Gaussian kernel."

Training and testing a variety of methods and models, for both feature selection and classification, will be the route most likely to provide a satisfactory solution.  What those particular methods and models will be is unknown at this point.

### Benchmark Model:  Logistic Regression

A logistic regression model will be used as the benchmark because it is a simple and common classification which will provide a base line to measure more sophisticated models against.

### Performance Metrics:  BER and AUC

The "Result Analysis" suggests the use of the balanced error rate (BER) and area under the ROC curve (AUC) as appropriate performance metrics.  Since *Madelon* results in a binary output, the "Results Analysis" considered BER = 1 - AUC.

Other considerations are the fraction of features selected and the fraction of probes found in the feature set selected.

### Citations

Lichman, M. (2013). UCI Machine Learning Repository [http://archive.ics.uci.edu/ml]. Irvine, CA: University of California, School of Information and Computer Science.

NIPS 2003 workshop on feature extraction. [http://clopinet.com/isabelle/Projects/NIPS2003/analysis.html]

Isabelle Guyon, 2003.  Design for experiments for the NIPS 2003 variable selection benchmark.

Isabelle Guyon, Steve R. Gunn, Asa Ben-Hur, Gideon Dror, 2004. Result Analysis of the NIPS 2003 Feature Selection Challenge.

Isabelle Guyon, Steve Gunn, Masoud Nikravesh, Lofti Zadeh (Eds.), Feature Extraction, Foundations and Applications. Studies in Fuzziness and Soft Computing. Physica-Verlag, Springer. 2006.

### Python Notebook with Associated *R* Code

The Python Notebook with associated *R* code can be found in the *ipynb* directory [attached to this GitHub repository.](https://github.com/seslezak/Madelon-Data-Set/blob/master/ipynb/01-data-description-ses.ipynb)

