# Codeless AI model building

Hands-on lab on how to build AI and ML models using a visual interface (no code) on Watson Studio and Watson Machine Learning. Tools used are Data Refinery and Modeler Flows, available on: Watson Studio Cloud / Local / Desktop and Machine Learning on Z.

## Exercise 0: Project setup and data loading

+ Create a project. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-project.png)

+ Download the data from [here.](https://ibm.box.com/s/cyiwthc06j0w9pi6bo2bvr77x8h26ara) 

+ Load the data to your project. To do so, click on the plus (+) sign at the top right corner and select "Add data set".
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/load-data.png)


## Exercise 1: Data curation

+ Create a modeler flow on your project under Assets. Give it any name and click "Create":
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-modeler-flow.png)

Flows allow you to drag and drop nodes and connect them. Each node could be a dataset, a transformation, or a model, among other things.

+ On the top right, click data panel (10101) and drag and drop the `airline.csv` dataset to the modeler flow. A new node "airline.csv" should appear on the canvas: 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/data-to-flow.png)


+ Under the Outputs Node List, drag and drop the "Data Audit" node.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/data-audit.png)


+ Connect the data node (airline.csv) to the Data Audit node. Right click on the Data Audit node and select "Run". To see the results, go to the top right corner and click the round arrow pointing down. You will see "Data Audit of [29 fields]". 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/connect-run.png)


+ Double click on "Data Audit of [29 fields]" and scroll down until you see the column "% Complete" which indicates the percentage of non-missing values per column.  Search for columns that are < 30% complete, i.e., more than 70% missing values. These should be:

- CarrierDelay
- WeatherDelay    
- NASDelay    
- SecurityDelay    
- LateAircraftDelay
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-missing.png)




+ Remove columns that have more than 70% missing values. To do so, drag and drop a Filter node (from Field Operations list) into the canvas and connect it to the Data node "airline.csv". Double click on the Filter node and then click on Filter on the collapsable menu on the right. Click on "Add Columns" to select the fields to filter out. Click Save.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/filter-out-fields.png)

+ Verify that the fields were filtered out by right clicking the Filter node then Preview. Scroll all the way to the right and make sure the intended fields were actually removed.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/preview-filter-out.png)

+ Remove cancelled or diverted flights. To do so, drag and drop a Select Node (from Record Operators) to the canvas. Connect it with the Filter node. Then, double click on it, go to Settings and create a condition, which will be "Cancelled = 1 or Diverted = 1".
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/select-flights.png)


## Exercise 2: Data exploration

+ Open the visualization tool. Go to your project, then Assets, then Data Sets, and  Data Assets select look for  `airline.csv`. Click on the three vertical dots menu and select click "Data Visualization" ![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/open-viz-tool.png)


+ Create a histogram of the flight arrival delay. Select the Histogram type, select column ArrDelay 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/hist-arrdelay.png)


+ Play with the histogram bin size. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/bin-size.png)


+ Plot flights per year using a histogram of the field Year. Unselect "Show distribution curve". Click Apply.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/hist-year.png)


+ Visualize busiest airlines using a barplot of column UniqueCarrier. Click Apply.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/busiest-airlines.png)


+ Visualize busiest airports using a barplot of column Origin. Click Apply.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/busiest-airports.png)


+ Visualize busiest times to fly with a histogram of departure time. Set "Bin width" to 2 to get hourly counts. Unselect "Show distribution curve"
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/busiest-time.png)


+ Draw a correlation plot using the Scatterplot matrix chart. Explore with different attributes such as ArrDelay and DepDelay. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/corr-plot.png)

Now let's go back to our Modeler Flow to do some more data exploration:

+ Compute correlations between ArrDelay and the rest of the columns. First, drag and drop the Statistics node (under Outputs) and connect it to the Select node. Double click on the Statistics node, go to Settings, and click on "Add Columns" under "Examine". Select the ArrDelay column and unselect all statistics. Under correlate click "Add Columns" and select all columns. Unselect the Show correlation strength labels in output. Click save. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/corr-arrdelay.png)


+ Right click on the Statistics node and click Run. See the results on the top right corner by clicking on the the round arrow pointing down and double click on Statistics. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-correlations.png)


## Exercise 3: Feature engineering

+ Create a new column "class" using the Derive node (under Field operations). Double click on it and go to Settings. Set the name for the new column as "class". Then set "Derive as" to "Nominal". Configure values as follows:
+ Early: if ArrDelay < 0.0, 
+ Delayed: if ArrDelay > 15.0,
+ On time: if ArrDelay >= 0.0 and ArrDelay <= 15.0
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-class-1.png) 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/create-class-2.png)


+ Plot the distribution of "class" using the Distribution Node (under Graph operations). 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/class-distribution.png)


+ Check the class distribution. Click the round arrow pointing down on the top right and double click the class distribution. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-class-dist.png)


+ Add a Type node (under Field operations) and change the class role to "target". 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/class-role-target.png) 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/class-role-target-2.png)

## Exercise 4: Modeling

+ Split data into train (80%) and test (20%) sets using the Partition node (under Field operations). 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/split.png)


+ Add a C5 Model node (under model operations). Right click and RUN to train the model. 
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


+ Connect a Table mode (under Output operations) to the train model. Right click and RUN. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/run-predictions.png)

+ To see the predictions of the class field, on the top right under the rounded pointing down arrow double click the most recent Table report . 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/see-predictions.png)

## Exercise 5: Deploy Model

+ Right click the trained model node and "Save as a model". 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/save-model.png)

+ Name your model and save. 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/name-model.png)

+ Go back to your project and look for your model. Under Actions, click "Publish". 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/publish-model.png)

+ On the published models (in the Models TAB), under actions, click "Deploy". 
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/click-deploy.png)

+ Name your deployment and click "create"
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/name-deploy.png)

+ Congratulations! Your model has been deployed as a web service. From here, you can check the deployment details, schedule evaluations with new labeled data, test the API and update models once trained with new data.
![](https://github.com/IBMDataScience/clickers/blob/master/screenshots/deployment.png)

