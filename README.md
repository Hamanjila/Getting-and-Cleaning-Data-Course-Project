# Getting-and-Cleaning-Data-Course-Project

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. This repo explains how all of the scripts work and how they are connected.
Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

# Create one R script called run_analysis.R does the following.

    *Merges the training and the test sets to create one data set.
    *Extracts only the measurements on the mean and standard deviation for each measurement.
    *Uses descriptive activity names to name the activities in the data set
    *Appropriately labels the data set with descriptive variable names.
    *From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity   and each subject.
    
# THE STEPS BELOW COMPLETE THE ASSIGNMENT AS PER INSTRUCTION
    
# Downloading and unzipping dataset

if(!file.exists("./data")){dir.create("./data")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl,destfile="./data/Dataset.zip")

# Unzip dataSet to /data directory
unzip(zipfile="./data/Dataset.zip",exdir="./data")

# 1. Merging the training and the test sets to create one data set:
# 1.1 Reading files

# Reading trainings tables:
x_train <- read.table("./data/UCI HAR Dataset/train/X_train.txt")
y_train <- read.table("./data/UCI HAR Dataset/train/y_train.txt")
subject_train <- read.table("./data/UCI HAR Dataset/train/subject_train.txt")

# Reading testing tables:
x_test <- read.table("./data/UCI HAR Dataset/test/X_test.txt")
y_test <- read.table("./data/UCI HAR Dataset/test/y_test.txt")
subject_test <- read.table("./data/UCI HAR Dataset/test/subject_test.txt")

# Reading feature vector:
features <- read.table('./data/UCI HAR Dataset/features.txt')

# Reading activity labels:
activityLabels = read.table('./data/UCI HAR Dataset/activity_labels.txt')

# 1.2 Assigning column names:

colnames(x_train) <- features[,2] 
colnames(y_train) <-"activityId"
colnames(subject_train) <- "subjectId"
      
colnames(x_test) <- features[,2] 
colnames(y_test) <- "activityId"
colnames(subject_test) <- "subjectId"
      
colnames(activityLabels) <- c('activityId','activityType')

# 1.3 Merging all data in one set:

mrg_train <- cbind(y_train, subject_train, x_train)
mrg_test <- cbind(y_test, subject_test, x_test)
setAllInOne <- rbind(mrg_train, mrg_test)

# 2. Extracting only the measurements on the mean and standard deviation for each measurement
# 2.1 Reading column names:

colNames <- colnames(setAllInOne)

# 2.2 Create vector for defining ID, mean and standard deviation:

mean_and_std <- (grepl("activityId" , colNames) | 
                 grepl("subjectId" , colNames) | 
                 grepl("mean.." , colNames) | 
                 grepl("std.." , colNames) 
                 )

# 2.3 Making nessesary subset from setAllInOne:

setForMeanAndStd <- setAllInOne[ , mean_and_std == TRUE]

# 3. Using descriptive activity names to name the activities in the data set:

setWithActivityNames <- merge(setForMeanAndStd, activityLabels,
                              by='activityId',
                              all.x=TRUE)

# 4. Creating a second, independent tidy data set with the average of each variable for each activity and each subject:
# 4.1 Making second tidy data set

secTidySet <- aggregate(. ~subjectId + activityId, setWithActivityNames, mean)
secTidySet <- secTidySet[order(secTidySet$subjectId, secTidySet$activityId),]

# 5.2 Writing second tidy data set in txt file

write.table(secTidySet, "secTidySet.txt", row.name=FALSE)


# Files

CodeBook.md describes the how to use all this, variables, the data, and any transformations or work that was performed to clean up the data.

run_analysis.R contains all the code to perform the analyses described in the 5 steps. They can be launched in RStudio by just importing the file.





