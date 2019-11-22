# clickers
hands on exercises for clickers using Data Refinery and Modeler Flows

## Create Project


## Download data and load it to your project


+ Download the data from here https://ibm.box.com/shared/static/negloqqqv21wx4hag2sml0h7zdj4pygs.csv
+ Load the data to your project [load-data]


## Create Modeler Flow and Start Data Exploration 


+ Create a modeler flow on your project, under Assets [create-modeler-flow]


+ On the top right, click data panel (10101) and drag and drop the `airline.csv` dataset to the modeler flow [data-to-flow]


+ Under the Outputs Node List, drag and drop the "Data Audit" node [data-audit]


+ Connect to data node, right click and run. On the top right click the round arrow pointing down, double click the audit node results and scroll down until you see a list of the percentage of the missing values on each column. [connect-run]


+ Search for columns that are < 30% complete [see-missing]
+    CarrierDelay
+    WeatherDelay    
+    NASDelay    
+    SecurityDelay    
+    LateAircraftDelay


+ Remove columns that have more than 70% missing values. Drag a Filter Node (from Field Operations list) and select the missing value fields to filter out. [filter-out-fields]
+  CarrierDelay
+  WeatherDelay    
+   NASDelay    
+    SecurityDelay    
+    LateAircraftDelay


+ Verify that the fields were filtered out bu right clicking the Filter node then Preview [preview-filter-out]


+ Remove cancelled or diverted flight by adding a Select Node with condition: Cancelled = 1 or Diverted = 1 [select-flights]


## Visualizations


+ Open the visualization tool. Go to your project, then Data Assets select the `airline.csv` and click "Data Visualization" [open-viz-tool]


+ Create a histogram of the flight arrival delay. Select the Histogram type, select column ArrDelay [hist-arrdelay]


+ Play with the histogram bin size. Bin size equal to 1 provides hourly delays. [bin-size]


+ Plot flights per year using a histogram of the filed Year. [hist-year]


+ Visualize busiest airlines using a Bar Plot of column UniqueCarrier. [busiest-airlines]


+ Visualize busiest airports using a Bar plot of column Origin. [busiest-airports]


+ Visualize busiest times to fly with a histogram of departure time. [busiest-time]


+ Draw a correlation plot using the scatter plot correlation type chart. [corr-plot]


## Back to Modeler to Train an ML Model


+ Compute correlations between ArrDelay and the rest of the columns. First drag and drop the Statistics node (under Outputs), select the ArrDelay column, unselect all statistics. Under correlate click "Add Columns" and select all columns. Unselect the Show correlation strength labels in output. Click save. [corr-arrdelay]


+ Right click the Statistics node and RUN. See the results on the top right under the rounded arrow pointing down and double-click Statistics. [see-correlations]


+ Create column "class" using the Derive node (under Field operations). Configure Values:
+ Early if ArrDelay < 0, 
+ Delayed if ArrDelay > 15,
+ On time 0 < ArrDelay < 15   [create-class-1] [create-class-2]


+ Plot the distribution of "class" using the Distribution Node (under Graph operations). [class-distribution]


+ Check the class distribution. Click the round arrow pointing down on the top right and double click the class distribution. [see-class-dist]


+ Add a Type Node (under Field operations) and change the class role to Target. [class-role-target] [class-role-target-2]


+ Split data into train (80%) and test (20%) sets using the Partition Node (under Field operations). [split]


+ Add a C5 Model Node (under model operations). Right click and RUN to train the model. [add-model]


+ Right click the output model and click the View Model option to get model details. Why do you think one single variable is getting all the importance? [view-model]


+ Go back to the Type node created a few steps back and change the ArrDelay and DepDelay columns' role to None (do the same for all the inputs that are not useful in practice). [adjust-type-node]


+ Inspect model's quality by connecting the Analysis ode to the yellow node (the trained model). Right click and run to see quality metrics like confusion matrix and accuracy on the train and test sets. [quality]


+ Open the quality metrics report by double clicking the Analysis report (under Output operations) on the top right under the rounded pointing down arrow. [open-quality] See how the accuracy and the confusion matrices change in train and test datasets. [see-quality]


+ Connect a Table Node (under Output operations) to the train model. Right click and RUN. [run-predictions] To see the predictions of the class field, on the top right under the rounded pointing down arrow double click the most recent Table report . [see-predictions]

