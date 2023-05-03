Download Link: https://assignmentchef.com/product/solved-cs373-homework-5-k-means
<br>
In this homework, you will be working with the ‘Yelp’ dataset. It contains 19 attributes: 15 diescrete and 4 continuous (<em>{</em><strong>latitude, longitude, reviewCount, checkins</strong><em>}</em>). We already did some exploring with this dataset in homework 1. Your task for this homework is to implement the k-means algorithm and apply it to the continuous attributes in the data.

Your submission will be run on a hidden dataset which is different from given dataset. The hidden dataset will have the same column names for the continuous attributes as the given dataset.

The features you will use are the 4 continuous attributes in yelp.csv.

<h2>1.2         Skeleton Code</h2>

You are provided a skeleton structure with this homework:

cs373-hw5/ handout.pdf data/ given/ yelp.csv

src/ init .py kmeans.py report/ report.pdf

<strong>Do not </strong>modify the given folder structure. You should not need to, but you may, add any extra files of code in cs373-hw5/src/ folder. You should place your report (report.pdf) in the cs373-hw5/report/ folder. You <strong>must not </strong>modify init .py. All your coding work for this homework must be done inside cs373-hw5/src/ folder. You are not allowed to use any external libraries for classifier implementations such as scikit-learn etc. Make sure that you understand the given code fully, before you start coding.

Your code will be tested using python2.7 from inside the cs373-hw5/src/ folder. If you wish to use python3.6, you need to place an empty file named ‘<strong>python3</strong>’ in your src/ folder. Make sure that you test your code on data.cs.purdue.edu before submitting.

<h2>1.3         Expected Output</h2>

Your python script should take three arguments as input:

<ol>

 <li>trainingDataFileName: corresponds to a subset of the data that should be used as the training set for your algorithm.</li>

 <li>K: the value of k to use when clustering.</li>

 <li>clustering option: takes one of the following five values, 1 (use the four original attributs for clustering, which corresponds to Q3.1), 2 (apply a log transform to reviewCount and checkins, which corresponds to Q3.2), 3 (use the standardized four attributes for clustering, which corresponds to Q3.3, 4 (use the four original attributes and Manhattan distance for clustering, which corresponds to Q3.4), and 5 (use 3% random sample of data for clustering, which corresponds to Q3.5).</li>

</ol>

Your code should read in the training sets from the csv file, cluster the training set using the specified value of k, and output the within-cluster sum of squared error and cluster centroids. For the centroid of each cluster report the values for each of the four attributes in the following order. <em>{</em><strong>latitude, longitude, reviewCount, checkins</strong><em>}</em>

The expected output is given below. Note that this will run your algorithm with the yelp.csv file, a K value of 4, and clustering option 1. Please make sure you follow this output else you <strong>WILL </strong>loose points. Note that this is only a sample output and the numbers are not representative of the actual results.

$ python kmeans.py yelp.csv 4 1 WC-SSE=15.2179

Centroid1=[49.00895,8.39655,12,3] …

CentroidK=[33.33548605,-111.7714182,9,97]

<strong>P.T.O</strong>

<h1>2           Kmeans</h1>

<h2>2.1         Theory</h2>

<ol>

 <li>(10 points) What are the benefits of the k-means clustering algorithm? What are the issues? In which situations should we use k-means? Your answer should compare to other algorithms learned in class (both unsupervised and supervised) in less than 4 sentences.</li>

</ol>

<h2>2.2         Implementation</h2>

You need to implement the k-means clustering algorithm for this part. This part could be completed by editing only kmeans.py. You need to follow the description of the models discussed in the lecture slides <a href="https://piazza.com/class_profile/get_resource/jqlonlli5gd3cb/ju8ht0oewhxrf">(link)</a> with the following specifications.

<strong>Features</strong>: Consider the 4 continuous attributes in yelp.csv for <strong>X</strong>.

<strong>Distance</strong>: Use Euclidean distance unless otherwise specified.

<strong>Score function</strong>: Use within-cluster sum of squared error (where <em>r<sub>k </sub></em>is the centroid of cluster <em>C<sub>k</sub></em>, d is the distance function.).

<em>K</em>

<em>wc</em>(<em>C</em>) = <sup>XX </sup><em>d</em>(<em>x</em>(<em>i</em>)<em>,r<sub>k</sub></em>)<sup>2                                                                                                                      </sup>(1)

<em>k</em>=1<em>x</em>(<em>i</em>)∈<em>C<sub>k</sub></em>

Make sure to also implement the following cluster options as described in Section 1.4.

<ol>

 <li>The four original attributes for clustering (corresponding to 3.1).</li>

 <li>A log transform to reviewCount and checkins (corresponding to 3.2).</li>

 <li>Standardize the 4 attributes for clustering (corresponding to 3.3).</li>

 <li>Four original attributes and Manhattan distance for clustering (corresponding to 3.4).</li>

 <li>A random sample of the data for clustering (corresponding to 3.5).</li>

</ol>

Report the results obtained on the given train set in your report.

<h1>3           Analysis</h1>

You only need to include your plots and discussions in your report. Make sure that the code you submit doesn’t include any changes you don’t want to be included.

<ol>

 <li>(10 points) Cluster the Yelp data using k-means.

  <ul>

   <li>Use a random set of examples as the initial centroids.</li>

   <li>Use values of K = [3,6,9,12,24].</li>

   <li>Plot the within-cluster sum of squares (wc) as a function of K.</li>

   <li>Choose an appropriate K from the plot and argue why you choose this particular K.</li>

   <li>For the chosen value of K, plot the clusters with their centroids in two ways: first using latitude longitude and second using reviewCount, checkins. Discuss whether any patterns are visible.</li>

  </ul></li>

 <li>(10 points) Do a log transform of reviewCount, checkins. Describe how you expect the transformation to change the clustering results. Then repeat the analysis (1). Discuss any differences in the results.</li>

</ol>

<strong>P.T.O</strong>

<ol start="3">

 <li>(10 points) Transform the four original attributes so that each attribute has mean = 0 and stdev = 1. You can do this with the numpy functions, numpy.mean() and numpy.std() (i.e., subtract mean, divide by stdev). Describe how you expect the transformation to change the clustering results. Then repeat the analysis (1). Discuss any differences in the results.</li>

 <li>(10 points) Use Manhattan distance instead of Euclidean distance in the algorithm. Describe how you expect the change in the clustering results. Then repeat the analysis (1). Discuss any differences in the results.</li>

 <li>(10 points) Take a 6% random sample of the data. Describe how you expect the downsampling to change the clustering results. Then run the analysis (i) five times and report the average performance. Specially, you should use a single random 6% sample of the data. Then run 5 trials where you start k-means from different random choices of the initial centroids. Report the average wc when you plot wc vs. K. For your chosen K, determine which trial had performance closest to the reported average. Plot the centroids from that trial. Discuss any differences in the results and comment on the variability you observe.</li>

 <li>(10 points) Improve the score function. To evaluate the clustering, it is not sufficient to measure only the within-cluster sum of squares (wc) that you used above. It is also desired to have each cluster separate from others as much as possible. To improve the resulting clustering, define your own score function that takes into account not only the compactness of the clusters but also the separation of the clusters. Write a formal mathematical expression of your score function and explain why you think your score function is better than the within-cluster sum of squares. Also, using the best configuration from Questions 1-5, plot the results of your score function for K = [3, 6, 9, 12, 24], and compare the results to the appropriate algorithm from Question 1-5.</li>

</ol>

<h1>4           Time Limit</h1>

Your code must terminate with in 8 minutes for each clustering model with 4 or less clusters. If it doesn’t terminate with in 8 minutes, you will be graded for the output your code generates at the end of the 8 minute time limit. If your code doesn’t converge by then, it would be a good idea to print the results you have at that point or use a different convergence criteria.