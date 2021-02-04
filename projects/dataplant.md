---
layout: project
type: project
image: images/dataex.png
title: Data Modelling Project
permalink: projects/dataplant
# All dates must be YYYY-MM-DD format!
date: 2019-12-16
labels:
  - R
  - Weka
  - Principal Component Analysis
  - Preprocessing
  - Analysis
  - Mining
  - Clustering
  - Classification
summary: A project in three parts, including data visualisation and preprocessing, clustering, and classification.
---

There were quite a few steps to this project, and I have abridged the instructions to focus more on my answers and analysis. At times, I was asked to explain topics or compare methods to show a deeper understanding. I used a provided dataset that is based on real-world plant data, but has been modified. It includes 18 attributes and a 724 instances (plants), each of which belong to a Class (revealed in the dataset).

The first section addresses data visualisation and pre-processing.

## Description, Visualisation, and Pre-Processing (R)
### 1a: Exploring the Data

I started by finding the centrality and dispersion measurements, as well as the number of missing values per attribute (not pictured).

### 1b: Exploring the Relationship Between Attributes and Between Attributes and Class

I then produced histograms for each attribute (Figure 1). As is my nature, I enjoyed exploring creative ways of doing things. After importing the attributes from the dataset, I wrote an algorithm to automate creation. It used the attribute column headers as titles on each histogram and a while statement with a variable (in this case 18, as there were 18 attributes) to determine when it should terminate.

I removed missing value and used the value of populated rows for each attribute to calculate custom bounds and binwidths for each attribute's histogram. So, first: I used this value to calculate the bounds of the x-axis, plus or minus one bind width, to make sure all bars were visible. Next: I used the value again in applying the Freedman-Diaconis rule for optimal binwidth, as there was not a one-size-fits-all value that would produce optimal bars. Watching all of the histograms fly by as the code ran was surprisingly exciting, as I spent a lot of time on this algorithm.

<div class="ui medium center floated rounded images">
<img class="ui image" src="../images/DMA images/1/histo cenx.png">
<img class="ui image" src="../images/DMA images/1/histo ceny.png">
<img class="ui image" src="../images/DMA images/1/histo mass.png">
<img class="ui image" src="../images/DMA images/1/histo width.png">
<img class="ui image" src="../images/DMA images/1/histo depth.png">
<img class="ui image" src="../images/DMA images/1/histo o0.png">
<img class="ui image" src="../images/DMA images/1/histo o1.png">
<img class="ui image" src="../images/DMA images/1/histo o2.png">
<img class="ui image" src="../images/DMA images/1/histo o3.png">
<img class="ui image" src="../images/DMA images/1/histo o4.png">
<img class="ui image" src="../images/DMA images/1/histo o5.png">
<img class="ui image" src="../images/DMA images/1/histo o6.png">
<img class="ui image" src="../images/DMA images/1/histo o7.png">
<img class="ui image" src="../images/DMA images/1/histo o8.png">
<img class="ui image" src="../images/DMA images/1/histo o9.png">
<img class="ui image" src="../images/DMA images/1/histo weight.png">
<img class="ui image" src="../images/DMA images/1/histo area.png">
<img class="ui image" src="../images/DMA images/1/histo hue.png"></div>
*Figure 1: Historgrams of Attributes.*
*Mean: Grey Double-Dashed; Median: Red Dashed; Mode: Blue Dotted Lines.*

I visualised the Class variable by colour and chose the [Viridis pallet](https://www.r-bloggers.com/2018/07/ggplot2-welcome-viridis/), as it's not only aesthetically pleasing, but also discernible to those with colour blindness. I represented the mean, median, and mode using colour-blind-safe colours, as well as different lines.

Considering the histograms along with the centrality and dispersion calculations in 1a, the x-axis reflects each attribute’s mean (normal distribution) or median (abnormal distribution) as the centre; range is the scale that the x-axis spans; standard deviation as where 2/3 of the data falls to the left or right of mean (normal distribution, only). The ideal normal distribution has the same mean, median, and mode.

Considering the data from the centrality and dispersion calculations, we should see this or very close to it for all Orientations, at least. However, examining the histograms, Orientation0, and Orientation5 have negative skews, while Orientation2, Orientation3, Orientation4, Orientation8, Orientation9, and Depth have positive skews. Outliers are most prominent for Orientations 2-4 and 7-9, as well as LeafArea and LeafHue. LeafWeight has the most dissimilar distribution, which is expected with over with half the instances missing. The distributions are generally normal and somewhat symmetrical for CentroidX, Width, Orientation1, Orientation6, Orientation7, LeafArea, and LeafHue. Exceptions to the above are possible bimodal distributions in CentroidY and Mass.

### 1b-i: Calculating Specific Correlations

According to the correlation coefficients: Orientation1 and Orientation7 have a very strong negative correlation-- when one attribute increases, the other decreases. Mass and Orientation0 have a very weak negative correlation, but we can make a reserved judgement that when one attribute increases, the other decreases. Orientation7 and Orientation8 have a very strong positive correlation-- when one attribute increases, the other does as well. Having examined 40% of the Orientation variables, we see the possibility that the Orientation attributes are dependent on each other, but not necessarily other variables.

> **Orientation1 and Orientation7:** -0.8696721\
> **Mass and Orientation0:** -0.08768968\
> **Orientation7 and Orientation8:** 0.9291126\

### 1b-ii: The Two Most Correlated Variables

> **Strongest Correlation-Orientation8 and Orientation9:** 0.9605505\
Having now examined 50% of the Orientation attributes and considering the results of 1Bi(iiii), the case for Orientation attributes having linear dependencies with each other is strengthened, though we cannot confidently comment on their relationship with non-Orientation attributes.

### 1b-iii: The Two Least Correlated Variables

> **Weakest Correlation-Depth and LeafArea:** 0.0005190327\
Having now examined 38% of the remaining non-Orientation attributes, the results indicate the possibility that non-Orientation attributes have weak or no correlation to other attributes and may be considered more “independent” than Orientation-related attributes.

### 1b-iv: Scatterplots of Class and Specific Attributes

<div class="ui large rounded images">
<img class="ui image" src="../images/DMA images/1/scatter o2 meh.png">
<img class="ui image" src="../images/DMA images/1/scatter o2 swap.png"></div>
*Figure 2: left- no jitter; right- jitter.*

Next, I was to produce scatterplots between the Class variable and Orientation 2, Depth, and Area. I used a Wes Anderson pallet on my scatterplots and adjusted the size and transparency of the dots to allow a visual representation of each class' density. Further, I adjusted the jitter, else the dots would lie atop each other, and I felt that did little to represent reality (Figure 2).

<img class="ui image" src="../images/DMA images/1/scatter o2 swap.png">
*Figure 3: Class and Orientation 2.*

Class compared with Orientation2 (Figure 3) varies the most of the three scatterplots. The points are in cluster-esque arrangements, with most points across all classes falling below the 0.14 measurement, and for A-D, below 0.13. Class E is the only Class with any points above 0.15. This indicates a low positive correlation, thus Orientation2 and Class have some dependency on each other.

<img class="ui image" src="../images/DMA images/1/scatter depth swap.png">
*Figure 4: Class and Depth.*

Examining the distribution of Class in the Depth attribute (Figure 4), there are apparent bands of points. There’s a marked decline in Depth as we examine the classes, with most points for A, B, and C toward the upper limit, then dropping in D and E. This indicates Depth has a negative correlation, and Depth and Class have a moderate negative dependency.

<img class="ui image" src="../images/DMA images/1/scatter larea swap.png">
*Figure 5: Class and Leaf Area.*

Class compared to LeafArea (Figure 5) has similar bands to Depth. Most points fall between 8,000 and 11,000, with each class having one or more bands outside this range. The points increase primarily within these bounds, indicating a low positive correlation and weak dependency between LeafArea and Class.

### 1c: General Conclusions

The most significant attributes are Orientation0, Orientation6, and Depth. Examining all correlations (calculated in 1b) along with other evidence (histograms, etc.), all Orientations have several moderate-to-strong correlations (±0.3-1.0). Orientation0 and Orientation6 have the most moderate-to-strong correlations (all Orientations and Depth). For non-Orientation attributes, Depth has the most moderate-to-strong relationships (CentroidY, Orientations 0-1, and Orientations 6-9). The least significant are CentroidX, LeafHue, and LeafWeight. CentroidX and LeafHue only have two moderate-to-strong correlations (CentroidX: Orientation2-3; LeafHue: Mass and LeafArea). LeafWeight has none, likely because it’s missing over half its instances, which is an indicator of insignificance on its own.

### 1d: Replacing the Missing Values with 0, Mean, and Median, and Comparing Approaches

Replacing missing data with zero, attribute means, or medians can be useful (referred to elsewhere as “Zeroset,” “Meanset,” and “Medianset,” respectively.), especially considering that many algorithms automatically drop any row or instance missing values. However, if several values are missing, results will be skewed. Other risks include outliers (rare: very high or low values), which affect means calculations; inadvertently weighting correlations between variables; or causing bias. Though outliers pose a risk, I think replacing missing values with means is the most useful of these three options.

### 1e: Attribute Transformation

When attributes are measured differently, it’s hard to compare them. Transforming them allows them to occupy the same scale, so they are comparable. MeanCenter performs centring, which subtracts the attribute’s mean from its column. Normalization subtracts the attribute’s minimum from its column, and divides that by the attribute’s range. The goal is to scale the attribute’s values from 0-1. Standardization centres and scales the attribute’s instances, with the goal of having a mean of 0 and standard deviation of 1. Scaling divides centred values by the attribute’s standard deviation. Each technique changes the scale of the x-axis and relocates the data on it. Y-axis changes are minimal.

I visualized LeafHue, as it has a mostly normal distribution (Figure 6; The original mean is 61.761, median is 61.838, and mode is 56.844). Of the techniques, normalization shows the least change in Class distribution amongst the bars. These techniques transformed the meanset and medianset’s means, medians, and modes to the same values (mean centering:0; standardization: 0; normalization: 0.004), which usually indicates a perfect-normal distribution of data. Examining the transformed datasets, we see why histograms of meanset and medianset’s mean centring and standardization look similar and normally distributed, while normalization doesn’t. Similarly, zeroset’s mean and median were transformed to 0 during mean centring and standardization, and 0.004 in normalization, though mode remains near the minimum (as mentioned before, I was concerned with skewing the data by replacing missing values with zero, and here we can see why, as significant outliers have been introduced).

<div class="ui medium rounded images">
<img class="ui image" src="../images/DMA images/1/lhue zero.png">
<img class="ui image" src="../images/DMA images/1/lhue mean.png">
<img class="ui image" src="../images/DMA images/1/lhue med.png">
<img class="ui image" src="../images/DMA images/1/mc zero.png">
<img class="ui image" src="../images/DMA images/1/mc mean.png">
<img class="ui image" src="../images/DMA images/1/mc med.png">
<img class="ui image" src="../images/DMA images/1/norm zero.png">
<img class="ui image" src="../images/DMA images/1/norm mean.png">
<img class="ui image" src="../images/DMA images/1/norm med.png">
<img class="ui image" src="../images/DMA images/1/std zero.png">
<img class="ui image" src="../images/DMA images/1/std mean.png">
<img class="ui image" src="../images/DMA images/1/std med.png"></div>
*Figure 6: Row 1- LeafHue, Original Generation of Zeroset, Meanset, Medianset.* \
*Row 2- Mean Centring on Zeroset, Meanset, Medianset.* \
*Row 3- Normalization on Zeroset, Meanset, Medianset.* \
*Row 4- Standardization on Zeroset, Meanset, Medianset.* \

### 1f: Attribute/Instance Selection
### 1f-i: Attribute and Instance Deletion Strategies for Missing Values

I examined the number of missing values in each column and row and decided outright to (programmatically) remove any attribute that had over 25% and any instance that had over 10% missing values. This left very few missing values in the data. I replaced these with the means of each attribute, similar to the example from section 1d-i (referred to as “Deletionset,” elsewhere).

### 1f-ii: Using Correlations to Reduce the Number of Attributes

I (programmatically) removed correlated attributes, which created a dataset of only LeafArea and LeafHue. I used na.omit to remove any missing values, which left 701 instances intact.

### 1f-iii: Using Principal Component Analysis (PCA) to Create a Dataset with Seven Attributes

I experimented with the raw data and missing values before deciding how to approach this. I found if I left the missing values in the data, I wasn’t able to perform prcomp, without using na.omit during it. Further, if I:
- …used na.omit during standardization, when projecting the data:
  - …manual projection resulted in 724 instances, but that is deceptive, as a great deal of missing values were reinstated during projection.
  - …projecting the returned values yielded 271 instances and no missing values.
    - Comparing the results, all the extant values returned in manual projection were the same as those in the returned values projection. The difference is reinstated NAs.
- …used na.omit prior to standardization:
  - …both approaches of projection had the same results: 271 instances.

Neither approach is ideal, as 63% of instances are lost. Regardless of approach, using na.rm during standardization didn’t change the results. Considering this, I again used the dataset created in 1f-i, deletionset. This left 704 instances and 17 attributes, which is an improvement. I also used the resulting values projection, rather than manual.

A simplistic way of explaining PCA is that each dimension/attribute is processed mathematically, then ranked based on the resulting variance. The first Principal Component (PC) is the transformed attribute that has the greatest variance. The second PC is found by assessing all dimensions that have no correlation to the first, then selecting the one with the greatest variance. Each subsequent PC is calculated in the same manner. Fortunately, *prcomp* performs all the equations and comparisons for us, both saving time and resulting in higher accuracy, for lack of human error.

I standardized the data, then calculated the PCs in a correlation matrix using *prcomp*, which I chose because *prcomp* uses singular value decomposition, giving more accuracy to results. Finally, I projected the data using the returned values. This reduced the dimensions, resulting in a dataset with only the specified number of Principal Components (7). I did this again for 10 PCs5, because such is required in Part 2.

I have summarized one way to perform PCA, without describing everything I could have explored during each step. However, considering a screeplot, cumulative screeplot plot, and summary for this dataset, I, personally, would have reduced to 8 Principal Components. 7 shows 93% variability; 10 shows 98%; but 8 shows 95%. After 95%, there is minimal variation to be achieved, therefore 8 is ideal.

## Part 2: Clustering (R)
### 2a: Using Hierarchical, K-Means, and PAM to Create Classifications

<img class="ui image" src="../images/DMA images/2/clustersx4 scale means.png">
*Figure 7: Initial Clustering Plots to Examine Effectiveness of Algorithms.*

<img class="ui small left floated rounded image" src="../images/DMA images/2/table scale means.PNG"> \
*Figure 8: Confusion Matrices of Initial Clustering Results.*

As K-Means clustering doesn’t allow missing values, I initially omitted them in advance. This left 271 instances amongst 18 variables, which I then scaled. This approach reduced all Class representations unevenly by 50-83%, so it wasn’t optimal. Considering this, I again used deletionset, which resulted in the removal of 20 instances (spread more evenly over each Class) and one attribute. I scaled the numeric data, added the Class attribute back in, then the clusters. I attempted several combinations of attributes for the x and y axes of the plots (Figure 7) and studied all pairs as plots to try to determine the best pairing. Clusplot uses PCA to determine the x and y variables for the plots, and colour codes the clusters by density (low to high: blue, green, red, purple). This is the way I prefer to visualize the plots.

Considering density, none of the plots match exactly, but PAM and K-Means most closely resemble the original densities (3 low, 2 high). Considering sizes, again, none match. K-Means is closest, and HCA and PAM are least similar, as both have one tiny cluster. Examining the confusion matrices (Figure 8), it’s hard to establish accuracy, as it’s not given that the predictions (1-5) automatically fall on the Class’ diagonal (A-E). Because of this, the predictions should be permuted to maximize the values along the diagonal. The diagonal’s sum is then divided by the total instances to establish each algorithm’s accuracy. This approach produced the following accuracies: HCA: 29%; K-Means: 39%; and PAM: 36%. With these observations in mind, K-Means still seems best approach.

### 2b: Exploring Optimisation Techniques

<img class="ui image" src="../images/DMA images/2/cluster test hca method.png">
*Figure 9: Hierarchical Clustering Methods*

I experimented with several adjustments for each algorithm. For HCA, I tried each method; K-Means, different, numbers of iterations (iter) and starts (nstarts), and algorithms; PAM, Euclidean and Manhattan Distances7, and standardization within the clustering algorithm. Examining these clusters as plots only hints at optimal tuning (Figure 10-12).

Note: The default for k-means is 10 iterations and 1 start, which I left intact, when they were not being modified for analysis (i.e., on any test that altered iterations, nstart was left at default, and both at default when testing algorithms). Euclidean Distance is measured by a straight line between two points, while Manhattan is executed by closing the distance using one or more right angles eventually connects two points, then measuring the distance.

<img class="ui image" src="../images/DMA images/2/cluster test km iter.png">
*Figure 10: K-Means Clustering, Iteration Experiments.*
<img class="ui image" src="../images/DMA images/2/cluster test km nstart.png">
*Figure 11: K-Means Clustering, NStart Experiments*
<img class="ui image" src="../images/DMA images/2/cluster test km algorithms.png">
*Figure 12: K-Means Clustering, Algorithm Experiments*


<img class="ui image" src="../images/DMA images/2/cluster test pam various.png">
*Figure 13: PAM Clustering, Various Experiments*

I had many more confusion matrices than in the previous section, thus it wasn’t as straightforward. A practical reason to examine confusion matrices is to discern clusters that aren’t visible on a plot, as is the case for HCA’s Single, Average, Median, and Centroid methods (Figure 9).

If this comes up in the future, I will use Rand Index, as it was developed for external cluster validation. However, I again measured accuracy via permutation of the diagonal values (Figure 14). An oddity is that the accuracy for K-Means 75, 100, and 200 starts are the same, but consulting the confusion matrices, this is an anomaly. From the results, I found for this dataset and algorithms:
- HCA:
  - Ward.D was the best method.
- K-Means:
  - iterations are most varied between 10 and 50, after which there isn’t much difference.
  - the number of starts peaked at 10 and accuracy didn’t increase much after 75.
  - Hartigan-Wong was the best algorithm.
- PAM:
  - Euclidean Distance differed only by 1% from Manhattan.
  - standardization didn’t make much difference.

  <img class="ui image" src="../images/DMA images/2/accuracy results.PNG">
  *Figure 14: Accuracy Results*

### 2c: Using One Clustering Technique on Alternative Datasets
I chose K-Means clustering using 50 iterations, 10 starts, and the Hartigan-Wong algorithm (Figure 15). I imagined PCAset would have the highest accuracy and zeroset the lowest, having expressed my opinion of both methods’ reliability elsewhere.

<img class="ui image" src="../images/DMA images/2/c4 clusters.png">
*Figure 15: K-Means Applied to PCAset, Deletionset, Zeroset, Meanset, and Medianset.*

<img class="ui image" src="../images/DMA images/2/cm kmeans.PNG">
*Figure 16: Confusion Matrices of K-Means Application.*

Though clusplot uses the first two Principal Components for the axes and I scaled each dataset, PCAset and zeroset’s points look different as do their scales, as their axes-components explain less than the others (Figure 16). As previously noted, replacing missing values with zero, means, or median can skew results, as seen on zeroset’s plot. Deletionset has the closest matching densities, but examining the confusion matrices, it has significantly less predicted instances in clusters 1 and 5. This is also true of zeroset’s predicted clusters 2 and 3; meanset’s cluster 4; and medianset’s clusters 3 and 4. From this, zeroset and medianset are unlikely to have the highest accuracies. The accuracy measurements (Figure 17) prove this supposition and my initial predictions to be true. Highest to lowest are: PCAset, deletionset, meanset, zeroset, and medianset.

<img class="ui image" src="../images/DMA images/2/c4 accuracy scale.PNG">
*Figure 17: Accuracy Results.*

## Part 3: Classification (Weka)

### 3a: Using ZeroR, OneR, NaïveBayes, IBk (k-NN), and J48 (C4.5) for Classification

FIGURE OUT THIS CHART
*Figure 18: Confusion Matrices and Abridged Classification Summaries for ZeroR, OneR, Naïve Bayes, and J48 Algorithms.*

For this dataset, J48 produced the best results (98.4%, Figure 18). I find it odd, but refreshing, to know two classifiers with very simplistic approaches (J48 and OneR) have the highest accuracies. I have given extremely cursory overviews of all methods employed below.
- ZeroR: a baseline classification that predicts the majority result from the training set.
  - If Class E is predicted, the training set had majority E-values.
- OneR: hypothesizes and tests a rule for each attribute based on class, choosing the one with the lowest error rate. That “one rule” is used to predict the other classes.
- Naïve Bayes: ignores dependencies and treats all variables as independent, giving equal weight to each attribute as an accurate predictor.
  - Predictions are based on results from the training set.
- IBk: predicts the class which an instance belongs to by the closest k-neighbour’s class.
- J48: builds a “tree” using entropy calculations to decide which attributes should be split into branches (>0 entropy), classed as nodes (highest gain), or leaves (0 entropy). Uses the constructed tree to classify.

### 3b: Choose One Algorithm to Explore Optimisation Techniques

Using IBk, I changed the number of k (introducing k-number of neighbours) to 1, 3, 5, and 10, and distance measurement to either Euclidean or Manhattan (Figure 19; Distances explained in previous note). With Euclidean Distance, the classifier’s accuracy decreased as k increased. There was an immediate increase just by changing the distance to Manhattan. Accuracy was 99.96% at 1 and 3 neighbours, then increased to 100% at 5 and 10.

<img class="ui image" src="../images/DMA images/3/multi ibk 1 3 5 10.PNG">
*Figure 19: IBk Results.* \
*Euclidean Distance with 1, 3, 5, 10 Neighbours, Respectively.* \
*Manhattan Distance with 1, 3, 5, 10 Neighbours, Respectively.*

Increasing k to 1, 10, 15, and 20 (Figure 24), Euclidean Distance’s accuracy increased at 20, while Manhattan Distance’s decreased after 15. Thus, the distance measurements have a substantial effect on the predictive ability, and accuracy can be fine-tuned by adjusting the number of k-neighbours.

<img class="ui image" src="../images/DMA images/3/multi ibk 1 10 15 20.PNG">
*Figure 20: IBk Results, Increased K-Neighbours.* \
*Euclidean Distance with 1, 10, 15, 20 Neighbours, Respectively.* \
*Manhattan Distance with 1, 10, 15, 20 Neighbours, Respectively.*

### 3c: Choose One Algorithm and Use if on Alternate Datasets

<img class="ui image" src="../images/DMA images/3/NB pca10 confusion matrix.PNG">
*Figure 21: Confusion Matrices and Abridged Classification Summaries for Dataset of 10 Principal Components ("PCAset").*

I used Naïve Bayes to classify the datasets and PCAset had the highest accuracy (Figure 21). Since PCA examines all attributes, orders them by highest to lowest variance, and allows us to discard any we find unimportant, PCA is beneficial for predicting potential trends in the data. At 10 PC (Figure 21), over 98% of variation is explained, so this dataset having the highest predictive ability is no surprise. Next, medianset is negligibly higher than meanset (Figure 22), followed by deletionset, (Figure 23) and the least accurate, as I suspected, was zeroset (Figure 22).

<img class="ui image" src="../images/DMA images/3/cm and classification deletionset.PNG">
*Figure 22: Confusion Matrices and Abridges Classification Summaries for Dataset with Missing Values Removed ("Deletionset").*

<img class="ui image" src="../images/DMA images/3/cm and classification others.PNG">
*Figure 23: Confusion Matrices and Abridges Classification Summaries for Datasets: Zeroset, Meanset, and Medianset.*

While meanset and medianset’s instance values would often be similar, I suspect medianset had better results, as medians aren’t susceptible to being skewed by outliers, unlike means. The outlier-skewing likely contributes to deletionset’s lower accuracy, as well, as I replaced missing instances with means. Lastly, zeroset introduces enough outliers to skew the dataset (reference: 1e) and is least likely to be an accurate representation of the data.
