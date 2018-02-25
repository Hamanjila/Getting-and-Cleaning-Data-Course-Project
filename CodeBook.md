# Overview
Source of the original data:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

Full Description at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

# The R script called run_analysis.R that does the following.

  1  Merges the training and the test sets to create one data set.
  
  2  Extracts only the measurements on the mean and standard deviation for each measurement.
  
  3  Uses descriptive activity names to name the activities in the data set.
  
  4  Appropriately labels the data set with descriptive variable names.
  
  5  From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
  
  #Variables:

    *x_train, y_train, x_test, y_test, subject_train and subject_test contain the data from the downloaded files.
    *x_data, y_data and subject_data merge the previous datasets to further analysis.
    *features contains the correct names for the x_data dataset, which are applied to the column names stored in

# secTidyData.txt

    *The first column contains subject IDs.
    *The second column contains activity names.
    *Subject IDs are integers between 1 and 30.
    *mean(): Mean value
    *std(): Standard deviation
    
#  About R script run from R Studio
Merging the training and the test sets to create one data set.
    * Reading files
    *Reading trainings tables
    *Reading testing tables
    *Reading feature vector
    *Reading activity labels
    *Assigning column names
    *Merging all data in one set
Extracting only the measurements on the mean and standard deviation for each measurement
    *Reading column names
    *Create vector for defining ID, mean and standard deviation
    *Making nessesary subset from setAllInOne
Using descriptive activity names to name the activities in the data set
Appropriately labeling the data set with descriptive variable names
Creating a second, independent tidy data set with the average of each variable for each activity and each subject
    *Making second tidy data set
    *Writing second tidy data set in txt file

