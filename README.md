<h1>What Drives the Price of a Car?</h1>
This python application will explore a dataset containing information on 3 millions used cars in order to determine which factors make a car more or less expensive. The current CRISP-DM Process Model for Data Mining (see Figure 1) will be followed.

</br>
</br>
<p align="center">
<img src="images/Figure1_CRISP_DM_Model.jpeg" width="300px" height="300px">
<h4 align="center"> Figure 1</h4>
</p>


<h2>Business Understanding</h2>
The Business task is to identify which factors make a car more or less expensive by using python & its libraries in jupyter notebook. This application will allow not only dealer tagging a price for a particular car that will be on the market, but also potential buyer to negociate a fair price for any particular car she/he/they is/are interested in.

<h2>Data Understanding</h2>
The dataset (vehicles.csv) given is in .csv format.It consists of 18 columns and 426880 rows as shown below (see Figure 2). The target columns is "price" which is numerical. there are only two more columns numerical: "odometer" and "year", i.e., the rest of the columns are categorical. Consequently, most of the dataset provided is imbalanced, suggesting that the modeling part will not be easy at some extend, specially considering the limitation regarding the cross-validation techniques that can be employed, and also the regression models options that can work in this particular case. All the columns, but "region", "price", and "state" contain a bunch of "NaN" values. Duplicates were not observed. It is thought that in order to provide  more insight into the aforementioned dataset, a data preparation, i.e, data cleaning process needs to be done first.

</br>
</br>
<p align="center">
<img src="images/figure2_data_1.jpeg" width="400px" height="500px">
<h4 align="center"> Figure 2</h4>
</p>

<h2>Data Preparation</h2>
The first step was to drop the null values (see Figure 3), and also make sure that there was not duplicates present in the dataset as well. As it is observed in Figure 4, all the columns now have same number of rows with no null values.

</br>
<p align="center">
<img src="images/figue2_data_4.jpeg" width="800px">
<h4 align="center"> Figure 3</h4>
</p>

</br>
<p align="center">
<img src="images/figure2_data5.jpeg" width="800px">
<h4 align="center"> Figure 4</h4>
</p>
</br>

Columns: "fuel", "cylinders", "type", and "transmission" have a feature with the same name: "other", so it was decided to replace it wiht different name to avoid potential problems in the foregoing analysis as indicated by Figure 5:

</br>
<p align="center">
<img src="images/figure2_data_6.jpeg" width="800px">
<h4 align="center"> Figure 5</h4>
</p>
</br>

Although the data preparation process is not totally completed, more insight into the dataset can be gained by doing the histograms for all categorical columns as shown on Figures 6, 7, 8, 9. The first observation is that there are two categorical data: ordinal and nominal. The second observation is that the categorical columns: "fuel", "manufacturer", "Condition", "size", "type", "drive", and "paint color" may be biased or driven by one predominant feature as indicated by their distribution dramatically skewed to the left. For instance, the presence of feature "gas" in the column 'fuel" is overwhelming, which is logical since most of cars are fueled by gas.

</br>
<p align="center">
<img src="images/figure2_histo1.jpeg" width="1000px">
<h4 align="center"> Figure 6</h4>
</p>

</br>
<p align="center">
<img src="images/figure2_histo2.jpeg" width="1000px">
<h4 align="center"> Figure 7</h4>
</p>

</br>
<p align="center">
<img src="images/figure2_histo3.jpeg" width="1000px">
<h4 align="center"> Figure 8</h4>
</p>

</br>
<p align="center">
<img src="images/figure2_histo4.jpeg" width="400px">
<h4 align="center"> Figure 9</h4>
</p>

<h4>Treatment of Outliers in Numerical Columns: "price", "odometer", and "year"</h4>
The presence of outliers in the numerical columns: 'price", "odometer", and "year" (see Figures 10, 12 and 12) indicated by the respective boxplot demands a careful and efective treatment in order to have to continue to the modeling phase. The histograms of the aforementioned columns have been also added for completeness.

</br>
</br>
<p align="center">
<img src="images/figure3_box1.jpeg" width="1000px">
<h4 align="center"> Figure 10</h4>
</p>

</br>
</br>
<p align="center">
<img src="images/figure3_box2.jpeg" width="1000px">
<h4 align="center"> Figure 11</h4>
</p>

</br>
</br>
<p align="center">
<img src="images/figure3_box3.jpeg" width="1000px">
<h4 align="center"> Figure 12</h4>
</p>

Two passes were applied to the aforementioned columns in order to remove the outliers. Before applying these two passes, values equal to 0 and 1 were removed from the column "price". The first pass consisted on applying the well known Inter quartile range (IQR) method, and the second passes consisted on appyling the DBSCAN ("Density-Based Spatial Clustering of Applications with Noise") method. Figure 13, 14, and 15 shows the final results after applying those two methods to remove the outliers. As it can be observed, the two passes were very effective, i.e., removing the majority of the outliers if any left. as an additional comments, the target column "price" shown a distribution skewed to the right, i.e, its logarithm version was used during the regression modeling by using the TransformedTargetRegressor tool.

</br>
</br>
<p align="center">
<img src="images/figure3_box1a.jpeg" width="1000px">
<h4 align="center"> Figure 13</h4>
</p>

</br>
</br>
<p align="center">
<img src="images/figure3_box2a.jpeg" width="1000px">
<h4 align="center"> Figure 14</h4>
</p>

</br>
</br>
<p align="center">
<img src="images/figure3_box3a.jpeg" width="1000px">
<h4 align="center"> Figure 15</h4>
</p>

Table 1 shows the final statistics of the target column "price":

</br>
<p align="center">
<img src="images/figure3_table1.jpeg">
<h4 align="center"> Figure 16</h4>
</p>

Once a effective work has been cpmpleted removing most or all of the outliers in the target column "price", boxplot "price" vs. the rest of the columns can be built as follows:



Observation: it is clear an upward trend, i.e. increases in both the median and the mean (white circular dot) of the price as year increases. Therefore, a positive correlation between these two variable can be expected.
