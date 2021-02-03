---
layout: project
type: project
image: images/dataex.png
title: Data Modelling Example
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

There were quicte a few steps to this project. The first section addresses data visualisation and pre-processing. 

## Descrption, Visualisation, and Pre-Processing (R)

###1a: Exploring the Data### 

I started by finding the centrality and dispersion measurements, as well as the number of missing values per attribute (not pictured). 

**1b** I then produced histograms for each attribute. As is my nature, I enjoyed exploring creative ways of doing things. After importing the attributes from the dataset, I wrote an algorithm to automate creation. It used the attribute column headers as titles on each histogram and a while statement with a variable (in this case 18, as there were 18 attributes) to determine when it should terminate. 

I removed missing value and used the value of populated rows for each attribute to calculate custom bounds and binwidths for each attribute's histogram. So, first: I used this value to calculate the bounds of the x-axis, plus or minus one bind width, to make sure all bars were visible. Next: I used the value again in applying the Freedman-Diaconis rule for optimal binwidth, as there was not a one-size-fits-all value that would produce optimal bars. Watching all of the histograms fly by as the code ran was surprisingly exciting, as I spent a lot of time on this algorithm.

I visualised the Class variable by colour and chose the Viridis pallet, as it's not only aesthetically pleasing, but also discernable to those with colour blindness. I represented the mean, median, and mode using colour-blind-safe colours, as well as different lines.

From my centrality and dispersion measurements, the x-axis relects each attribute's mean (normal distribution) or median (abnormal distribution) as the centre; the range is the scale that the x-axis spans; standard deviation is where 2/3 of the data falls to the left or right of the mean (in normal distrubtion only). The ideal normal distribution has the same mean, median, and mode. According to the centrality and dispersion measurements, I expected all attributes to adhere to this, but, once visualised, I saw my expectation was not true. Orientations 0 and 5 have negative skews; Orientations 2, 3, 4, 8, 9, and Depth have positive skews; there are prominent outliers is Orientations 2-4 and 7-9, as well as Leaf Area and Hue. Leaf Weight had the most dissimilar distribution, which is not surprising, as over half its instances were missing in the dataset. The distributions of Centroid X, Width, Orientations 1, 6, 7, Leaf Area, and Hue are generally normal and symmetrical. There are possible bimodal distributions for Centroid Y and Mass.

**1b-i** After histograms, I was tasked with examining the correlation coefficients of Orientations 1 and 7 (strong negative correlation), Mass and Orientation 0 (weak negative correlation), and Orientation 7 and 8 (very strong positive correlation). From examining only these three pairs, we might predict that the Orientation attributes are dependent on each other, but not necessarily other attributes.

**1b-ii** In examining all attributes for correlation, I found Orientation 8 and 9 to have the strongest correlation, strengthening my previous assertion of dependency. 

**1b-iii** The weakest correlation is Depth and Leaf Area, which, again, implies little or no dependency of Orientation-attributes on non-Orientation attributes.

**1b-iv** Next, I was to produce scatterplots between the Class variable and Orientation 2, Depth, and Area. I used a Wes Anderson pallet on my scatterplots and adjusted the size and transparency of the dots to allow a visual representation of each class' density. Further, I adjusted the jitter, else the dots would lie atop each other, and I felt that did little to represent reality.

In examining the scatterplots for Class and Orientation 2, the cluster-esque arrangements are obvious, with most points across all classes falling below the 0.14 measurement, and, for A-D, below 0.13. Class is the only class with any points above 0.15. This indicates a low-positive correlation, thus Class and Orientation 2 have some dependency on each other. 

For the distribution of Class and Depth, there are apparent bands of points this time. There's a marked decline in Depth as we examine the classes, with most points for A, B, and C toward the upper limit, then declining in D and E. This indicates Depth has a negative correlation, and Class and Depth have a moderate-negative dependency, indicating possible dependency.

Last, comparing Class and Leaf Area, the scatterplot has similar bands to Depth. Most points fall between 8,000 and 11,000, with each class having one or more bands outside this range. The points increase primarily within these bounds, indicating a low-positive correslation, thus a weak dependency between Class and Leaf Area. 

**1c** In considering all correlations along with other evidence, such as the histograpms, the most significant attributes are Orientations 0 and 6, and Depth. While all of the Orientation-attributes have several moderate-to-strong correlations (±0.3-1.0), Orientations 0 and 6 have such with all other Orientations, as well as Depth. For non-Oriengation attributes, Depth has the most moderate-to-strong relationships (CentroidY, Orientations 0-1, and Orientations 6-9). The least significant are CentroidX, LeafHue, and LeafWeight. CentroidX and LeafHue only have two moderate-to-strong correlations (CentroidX: Orientation2-3; LeafHue: Mass and LeafArea). LeafWeight has none, likely because it’s missing over half its instances, which is an indicator of insignificance on its own.

##


