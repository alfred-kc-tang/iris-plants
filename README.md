# [K-Means Clustering on Iris Plants](https://alfred-kctang.github.io/iris-plants/)

## Table of Contents

* [Goal](#goal)
* [Data Source](#data-source)
* [Methodology](#methodology)
* [Findings](#findings)
* [Keywords](#keywords)
* [Coding Style](#coding-style)
* [License](#license)

## Goal

This project aims at showcasing one of the popular unsupervised learning techniques, k-means clustering, on the famous iris data set.

## Data Source

The data set is obtained from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Iris), but it can also be accessed in R.

## Methodology

K-means clustering groups data points into a predefined number of clusters. Oftentimes, the algorithm started with a random set of centroids, i.e. as the centers of the clusters. Then it iterates the following two steps back and forth until convergence: (1) count data points into the cluster whose centroid is nearest to them, (2) each of the centroids is redefined as the mean of the data points in its corresponding clusters.

As the algorithm is usually set to terminate when the centroids are no longer changed, i.e. no point belongs to a cluster whose centroid is closer than the centroid of its current cluster. That is to say, it terminates only when it converges to a local optimum with the least within-cluster sum of squares by its very design. In any case, it can be proved that the algorithm converges to a local optimum in finite steps. We can see how the algorithm groups the data into clusters in the following GIF: 

<p align="center">
  <img src="https://github.com/alfred-kctang/iris-plants/blob/master/kmeans.gif?raw=true" alt="pkmeans animation"/>
</p>

## Findings

<p align="center">
  <img src="https://github.com/alfred-kctang/iris-plants/blob/master/elbow_diagram.png?raw=true" alt="elbow diagram"/>
</p>

In order to find the best value of k, I used the available component “tot.withinss”, i.e. total within-cluster sum of squares, given by the k-means function. It gives the sum of distances between each point and the mean of the cluster it is assigned to for each of the models with different k values from 1 to 15. Here I used the sapply function, which uses vectorized operations instead of for loops to make code faster and more concise, to try out these different values of k. By plotting the total within-cluster sum of squares on the y-axis versus the number of k on the x-axis, the elbow diagram is shown above.

As the elbow diagram indicates, there are significant decreases up to 3, after which decreases are much slower. So I would pick 3 as the best value of k, as it is the highest value of k after which diminishing returns occur. The prediction accuracy of the model is 0.83.

However, I went one step further to perform variable selection in order to see if it can boost the performance of the model. Since there are only four explanatory variable in the data, it is easy to try out all the possible combinations of predictors (but fixing k as 3; otherwise, the combinations would be much larger). It turns out that  models using only variable 4 or the combination of variables 3 and 4 have the best performance with the accuracy of 0.96. By Occam’s razor, the best model is the one that uses explanatory variable 4.

## Keywords

clustering, k-means clustering, unsupervised learning, variable selection

## Coding Style

This projects follows [Google's R Style Guide](https://google.github.io/styleguide/Rguide.html), which is a fork of the [Tidyverse Style Guide](https://style.tidyverse.org/) by Hadley Wickham.

## License

This repository is covered under the [MIT License](https://github.com/alfred-kctang/iris-plants/blob/master/LICENSE).
