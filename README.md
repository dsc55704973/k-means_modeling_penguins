# k-means_modeling_penguins
I made a K-means model to cluster data from a dataset of a sample size of 345 penguins, with datapoints such as species, origin island, and sex, as they relate to a study by PLOS ONE of sexual dimorphism among penguins (essentially, physical differences between males and females of the same species).

K-means is a popular clustering algorithm used in data analysis and machine learning. It partitions a set of data points into a specified number of clusters (denoted as "k") such that each data point belongs to the cluster with the nearest mean value. The algorithm iteratively assigns points to clusters based on the proximity to the mean or centroid of each cluster, and then recalculates the centroids until the positions of the centroids stabilize, indicating that the clusters are as coherent and distinct as possible. This method is often used for segmenting data, pattern recognition, and image analysis.

K-means is a great starting point for understanding unforseen patterns that may not be immediately obvious during exploratory data analysis, and can be leveraged as an engineered feature for more robust models.  In this exercise, I did not proceed to advanced modeling--I solely sought to exhibit my skill in designing a k-means model and evaluating the results.  Please review my code for a more in-depth look at my process, but I will cover it high-level in this README file.

To begin, I simply exlpored and cleaned up the data a bit in order to satisfy the assumptions of k-means modeling.  One important assumption is that the data is normalized, so I used Scikit-Learn's StandardScaler() to scale each datapoint (scaling essentially takes each datapoint and subtracts the mean observed value of the feature and divides it by the standard deviation, thus unsuring all variables have a mean of 0 and variance/standard deviation of 1.  Furthermore, k-means modeling assumes that there are no missing values, so I dropped those.  Lastly, I dropped the 'island' column as it was a useless feature and encoded the 'sex' feature.

Next, I utilized some helper functions to compute inertia and silhouette scores and put them into lists, which I then used to vizualize on line plots.  

Clustering by Inertia:

<img width="458" alt="Exhibit C Clustering by Inertia" src="https://github.com/dsc55704973/k-means_modeling_penguins/assets/66639071/f26353c1-13f0-46ae-8534-bd635dc7861e">

Clustering by Silhouette Score:

<img width="456" alt="Exhibit D Clustering by Silhouette Score" src="https://github.com/dsc55704973/k-means_modeling_penguins/assets/66639071/dbfd6898-ce09-4884-95e6-d9e1a945b8c2">

With these line plots, I was then able to leverage the "elbow method" to ascertain any obvious optimal value for "k" (number of clusters), which was 6 clusters.

Optimal K-Value:

<img width="891" alt="Exhibit A Optimal K-Value" src="https://github.com/dsc55704973/k-means_modeling_penguins/assets/66639071/d6b8d818-47ba-4ff3-b7e7-b57b341ec00a">

From there, it was simple enough to plug this k-value into my k-means model.  After running this model, I then added generated the k-means labels and added them back to the unscaled dataframe (it's often easier to interpret the results of clustering on unscaled data).  

Cluster Indexed Dataframe:

<img width="628" alt="Exhibit B Cluster Indexed Dataframe" src="https://github.com/dsc55704973/k-means_modeling_penguins/assets/66639071/3fa91f26-2b83-437c-a843-174b3e9291f0">

I then proceeded to determination of which features had the greatest cluster differentiation using groupby(), and visualizing these aggregations with barplots (I focused on species and sex only).

Clusters Differentiated by Species:

<img width="403" alt="Exhibit E Clusters Differentiated by Species" src="https://github.com/dsc55704973/k-means_modeling_penguins/assets/66639071/4a11c094-dc6c-4a51-a00c-eda1cb9a5eef">

Clusters Differentiated by Sex:

<img width="411" alt="Exhibit F Clusters Differentiated by Sex" src="https://github.com/dsc55704973/k-means_modeling_penguins/assets/66639071/ee007e8b-7ec3-4d92-82f1-65eb1d105ab4">

Ultimately, this process led me to the final determination that the clusters are best differentiated by sex, given that each cluster had the least diversity (each cluster was either exclusively male, or exclusively female).  The model also had pretty strong differentiation by species.  With this new feature, we may proceed to more robust feature engineering and advanced modeling, and have a better understanding of the natural grouping of the data. 

