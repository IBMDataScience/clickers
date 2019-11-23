# Codeless AI model building.

This repository contains examples on how to build AI and ML models using a visual interface and with no need to write a single line of code.

Tools used are Data Refinery and Modeler Flows, available on:
- Watson Studio Cloud
- Watson Studio Local
- Watson Studio Desktop
- Watson Machine Learning on Z
- SPSS Modeler

## Step 1: Data loading

+ Create a project. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-project.png)

+ Download the data from [here](https://ibm.box.com/shared/static/negloqqqv21wx4hag2sml0h7zdj4pygs.csv)

+ Load the data to your project 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/load-data.png)


## Step 2: Data Exploration

+ Create a modeler flow on your project, under Assets 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-modeler-flow.png)

Flows allow you to drag and drop nodes and connect them. Each node could be a dataset, a transformation, or a model, among other things.

+ On the top right, click data panel (10101) and drag and drop the `airline.csv` dataset to the modeler flow 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/data-to-flow.png)


+ Under the Outputs Node List, drag and drop the "Data Audit" node 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/data-audit.png)


+ Connect to data node, right click and run. On the top right click the round arrow pointing down, double click the audit node results and scroll down until you see a list of the percentage of the missing values on each column. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/connect-run.png)


+ Search for columns that are < 30% complete 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-missing.png)
+    CarrierDelay
+    WeatherDelay    
+    NASDelay    
+    SecurityDelay    
+    LateAircraftDelay


+ Remove columns that have more than 70% missing values. Drag a Filter Node (from Field Operations list) and select the missing value fields to filter out. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/filter-out-fields.png)
+  CarrierDelay
+  WeatherDelay    
+   NASDelay    
+    SecurityDelay    
+    LateAircraftDelay


+ Verify that the fields were filtered out by right clicking the Filter node then Preview 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/preview-filter-out.png)


+ Remove cancelled or diverted flight by adding a Select Node with condition: Cancelled = 1 or Diverted = 1 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/select-flights.png)


## Visualizations


+ Open the visualization tool. Go to your project, then Data Assets select the `airline.csv` and click "Data Visualization" ![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/open-viz-tool.png)


+ Create a histogram of the flight arrival delay. Select the Histogram type, select column ArrDelay 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/hist-arrdelay.png)


+ Play with the histogram bin size. Bin size equal to 1 provides hourly delays. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/bin-size.png)


+ Plot flights per year using a histogram of the filed Year. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/hist-year.png)


+ Visualize busiest airlines using a Bar Plot of column UniqueCarrier. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/busiest-airlines.png)


+ Visualize busiest airports using a Bar plot of column Origin. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/busiest-airports.png)


+ Visualize busiest times to fly with a histogram of departure time. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/busiest-time.png)


+ Draw a correlation plot using the scatter plot correlation type chart. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/corr-plot.png)


## Back to Modeler to Train an ML Model


+ Compute correlations between ArrDelay and the rest of the columns. First drag and drop the Statistics node (under Outputs), select the ArrDelay column, unselect all statistics. Under correlate click "Add Columns" and select all columns. Unselect the Show correlation strength labels in output. Click save. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/corr-arrdelay.png)


+ Right click the Statistics node and RUN. See the results on the top right under the rounded arrow pointing down and double-click Statistics. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-correlations.png)


+ Create column "class" using the Derive node (under Field operations). Configure Values:
+ Early if ArrDelay < 0, 
+ Delayed if ArrDelay > 15,
+ On time 0 < ArrDelay < 15   
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-class-1.png) 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-class-2.png)


+ Plot the distribution of "class" using the Distribution Node (under Graph operations). 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/class-distribution.png)


+ Check the class distribution. Click the round arrow pointing down on the top right and double click the class distribution. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-class-dist.png)


+ Add a Type Node (under Field operations) and change the class role to Target. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/class-role-target.png) 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/class-role-target-2.png)


+ Split data into train (80%) and test (20%) sets using the Partition Node (under Field operations). 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/split.png)


+ Add a C5 Model Node (under model operations). Right click and RUN to train the model. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/add-model.png)


+ Right click the output model and click the View Model option to get model details. Why do you think one single variable is getting all the importance? 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/view-model.png)


+ Go back to the Type node created a few steps back and change the ArrDelay and DepDelay columns' role to None (do the same for all the inputs that are not useful in practice). 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/adjust-type-node.png)


+ Inspect model's quality by connecting the Analysis ode to the yellow node (the trained model). Right click and run to see quality metrics like confusion matrix and accuracy on the train and test sets. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/quality.png)


+ Open the quality metrics report by double clicking the Analysis report (under Output operations) on the top right under the rounded pointing down arrow. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/open-quality.png) 

+ See how the accuracy and the confusion matrices change in train and test datasets. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-quality.png)


+ Connect a Table Node (under Output operations) to the train model. Right click and RUN. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/run-predictions.png)

+ To see the predictions of the class field, on the top right under the rounded pointing down arrow double click the most recent Table report . 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-predictions.png)

