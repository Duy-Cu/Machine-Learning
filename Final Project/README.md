
# Machine-Learning-Project
Creates 4 different regression models from Gas Turbine CO and NOx Emission Dataset


## Data Set Description
The datasets consists of year 2011-2015. Each excel sheet has around 7,000 datasets with 9 inputs and 2 outputs (Yellow). The output can be combined (by sums) with proper multiplier to produce one output. In this case, we will multiply CO by 26.5 to produce similar significance as NOX. The reason is that they both have the same units and are both harmful chemicals that needs to be monitored. The data are sorted in a chronological order of a 1 hour readings (by average). This means a dataset is formed by averaging the readings from sensors in a 1 hour frame period. Each sheet of the data folder consists of around 7,200 datasets, which is roughly close to total hours within a year (a year consists of 8736 hours). The missing hours are assuming that the turbine was offline for quality controls/maintenance. (The 'Ambient' features can be used quite well to predict energy yield [TEY])
![image](https://user-images.githubusercontent.com/37159143/118859398-0940ae00-b88f-11eb-822c-54a29c7d5139.png)


## Data Set Visualization
We will explore the statistics for each dataframe and determine which model we should go with.
![image](https://user-images.githubusercontent.com/37159143/118859620-4ad15900-b88f-11eb-97c6-7e47341d9634.png)
![image](https://user-images.githubusercontent.com/37159143/118859627-4d33b300-b88f-11eb-9a2d-57106264d857.png)
![image](https://user-images.githubusercontent.com/37159143/118859612-46a53b80-b88f-11eb-871f-b020ba6074e1.png)


## Data Set Cleaning
We will remove any features & response that falls out of the range of:<br /> 
[Q1\ -\ k·IQR,Q3 - k·IQR]<br />
Total datasets before: 36,733<br />
Total datasets after: 28,503<br />
<br />
With k=1.5, we lost ~8,000 datasets. We will use  k=2 instead to reduce data loss.<br />
Total datasets before: 36,733<br />
Total datasets after: 31,107<br />
<br />
Now we only loss ~5,000 datasets, which is not that bad.


## Related Research
### How Support Vector Regression works:<br />
Attempt to generate ‘hyperplanes’ that separates the data based on different response. The dimension will be based on the number of inputs (this case its 9 dimensional). One ‘hyperplane’ equation is: <br />
\beta_0+\beta_1X_1+\beta_2X_2+\ldots+\beta_pX_p=0<br />
<br />
This is then used as a prediction whether a set of inputs will belong to a specific response or not.<br /> 
Note: MMC (Maximum Margin Classification) is used for only Classification models but not for regression problem

### How Decision Tree Regression works:
This algorithm will generate a tree-like decisions. From a graphical perspective, it splits into rectangular regions (features as the axis). 

It is important that this algorithm requires ‘pruning’ to optimize both performance and run time. Pruning the decision tree means setting limitations on the tree size. This requires removing Internal nodes and thus produce terminal nodes. Image below shows an example of Decision Tree model:
![image](https://user-images.githubusercontent.com/37159143/118860184-f24e8b80-b88f-11eb-8dca-1725cf8f2a25.png)


## R-squared & MSE Metrics Explained:
### What does R-Squared tell us:
R-squared tells us how well the predicted model fits with the datasets. This measures the model performance of the model, which gives the strength of the relationship of the model to the response. However, R-squared does have some blindsides. <br />
Equation:<br />
R^2=\frac{\mathrm{TSS} -\mathrm{RSS} }{\mathrm{TSS}}<br />
Where:<br />
\mathrm{TSS}=\sum\left(y_i-\bar{y}\right)^2,\ \ RSS=\sum_{i=1}^{n}\left(y_i-\widehat{y_i}\right)^2<br />
<br />
Some limitations of R-Squared:<br />
- Cannot determine the biased of the prediction and coefficients parameter.
- Does not necessary indicate fitted model. It is possible that the overall average error of each datapoint is close to zero, but it is possible that each point is extensively away from the fitted prediction. 


### What does MSE tell us:
MSE is a performance metrics of the model. The way MSE is calculated is like R-squared, but only focus on the error terms between the model prediction and the actual response.<br />
Equation:<br />
MSE=\frac{1}{n}\sum_{i=1}^{n}\left(y_i-\hat{f}\left(x_i\right)\right)^2



## Feature Extraction 
We will be using PCA to reduce the number of features. Raw datasets have 9 features, if we can reduce this number, we can improve compute power significantly. PCA will perform much better when we consider scaling the features beforehand. 

CO performance (using the raw 9 features):<br />
![image](https://user-images.githubusercontent.com/37159143/118860778-a223f900-b890-11eb-95b3-fb9410c2002c.png)

PCA with 5 dimensions and CO performance:<br />
![image](https://user-images.githubusercontent.com/37159143/118860619-786ad200-b890-11eb-9d4c-2cd70444cb67.png)
![image](https://user-images.githubusercontent.com/37159143/118860629-7bfe5900-b890-11eb-84e7-c9c24b6396fe.png)


<br />
PCA with 6 dimensions and CO performance:<br />



<br />
PCA with 7 dimensions and CO performance:<br />


<br />
Using PCA with 7 component seems to give good performance and reduced run time compared to running with the raw inputs.







