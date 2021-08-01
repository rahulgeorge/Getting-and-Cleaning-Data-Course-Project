# This is the Code Book for project submission
CodeBook done by Rahul George as part of Getting and Cleaning Data Course Project.

## Generating Tidy Data 
Plainly executing the R Script will be sufficient to generate the tidy data (tidyData.txt) as required by the final step in the project. The script downloads, unzips and processes the data as described below to generate the final tidy data output.

## Source Data Information
The source data is from Human Activity Recognition Using Smartphones Data Set under The UCI Machine Learning Repository. Complete information about the dataset can be obtained from the [Original Source](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones). Data can be directly downloaded from this [Original Source](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip).

## About R Script
R Script performs a total of 5 actions as required by the project. Each process is explained below with its role in processing the data. Please note that Step 4 requested by the project is done as first step to easily work with data.

###### **Action 4** Labeling dataset with descriptive variable names
Both training and testing data is labelled using information in features.txt document. y & subject documents are labelled `activityID` and `subjectID`. `activityLabels` read from activity_labels.txt document is labelled as `activityID` & `activityType`. 

Action 4 is done in the beginning to make the rest code of the code more readable.

###### **Action 1** Merges the training and the test sets to create one data set.
Testing and training data is individually column binded in the order y, subject & x. Testing and training data is then merged using row bind to generate a single Dataset. The variable `CompleteData` contains the merged complete dataset.

###### **Action 2** Extracting Mean & Standard Deviation
`grepl()` function is used to search the dataset's column names for mean and std. The output vector is then modified to include the Activtiy ID and Subject ID columns. The final Dataset with just the mean and standard deviation columns are stored in the variable `meanStdData`.

###### **Action 3** Adding Descriptive Activity Names
`meanStdData` generated in **Action 2** is merged with `activityLabels` variable to add descriptive activity names.

###### **Action 5** Creating an independent data set with the average of each variable for each activity and subject
library `dplyr` is used to group the labelled dataset in **Action 3** by `activtityType` & `subjectID`. The grouped tbl is then processed through `summarise_all()` function to find mean for all the columns. The output is then written into a text file named `tidyData.txt`.

All the processing is conducted within a folder created by the script called `workingData` within the default working directory.
