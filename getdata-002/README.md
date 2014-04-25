# Getting and Cleaning Data(Peer Assessment)

## Introduction

This repository is created specially for Peer Assessment in "Getting and Cleaning Data" course,
which is managed by [Coursera Website](https://class.coursera.org/getdata-002).

## Guide

To run my code you can download this file **[run_analysis.R]()** or copy code below and paste it into R, and then import it using ```source('~/data/run_analysis.R')``` command,
finally after import, call function **start_dancing()** without any parameters.
The **start_dancing()** function will return, print & save the final result to ```./data/tidyData.csv```.

**Note**: output is saved to file [tidyData.csv]() & to understand data structure of **tidyData.csv** you should read this [CodeBook.md]().

## Code

```{r}
p <- function(...){
  return(paste(..., sep=""))
}

watch <- function(label, data){
  print(p(label, " Rows: ", length(data), " - Cols: ", length(names(data))))
}

start_dancing <- function(){
  
  # Change Working Directory to User Home Folder
  setwd("~") # linux/Mac
  
  #switch(Sys.info()[['sysname']],
  #Windows= {print("I'm a Windows PC.")},
  #Linux  = {print("I'm a penguin.")},
  #Darwin = {print("I'm a Mac.")})
  
  # Make data Directory
  if(!file.exists("./data")){
    dir.create("./data")
  }
  
  # Download Project File
  if(!file.exists("./data/getdata-projectfiles-UCI HAR Dataset.zip")){
    print("Project File not Exist, Downloading...")
    URL <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
    download.file(URL, destfile="./data/getdata-projectfiles-UCI HAR Dataset.zip", method="curl")  
    print("Project File not Exist, Downloading. [DONE]")
  }else{
    print("Project File Existed.")
  }
  
  # Unzip Project File
  if(!file.exists("./data/UCI HAR Dataset")){
    print("Project File is in zip format, unzipping...");
    unzip("./data/getdata-projectfiles-UCI HAR Dataset.zip", exdir="./data")
    print("Project File is in zip format, unzipping. [DONE]");
  }else{
    print("Project Directory is Ready.");
  }
  
  # Load Features
  print("Loading Features data...")
  features <- read.table("./data/UCI HAR Dataset/features.txt", header=F)
  print("Loading Features data. [DONE]")
  
  # Load Activity Labels
  print("Loading Activity Labels data...")
  activity_labels <- read.csv("./data/UCI HAR Dataset/activity_labels.txt", header=F, sep=" ")
  names(activity_labels) <- c("id", "name")
  
  print("Loading Activity Labels data. [DONE]")
  
  # Load Test
  print("Loading Test data...")
  subject_test <- read.csv("./data/UCI HAR Dataset/test/subject_test.txt", header=F)
  names(subject_test) <- "subject"
  
  X_test <- read.table("./data/UCI HAR Dataset/test/X_test.txt", header=F)
  names(X_test) <- features$V2
  y_test <- read.csv("./data/UCI HAR Dataset/test/y_test.txt", header=F)
  names(y_test) <- "y"
  
  body_acc_x_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/body_acc_x_test.txt", header=F)
  #names(body_acc_x_test) <- "body_acc_x"
  body_acc_y_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/body_acc_y_test.txt", header=F)
  #names(body_acc_y_test) <- "body_acc_y"
  body_acc_z_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/body_acc_z_test.txt", header=F)
  #names(body_acc_z_test) <- "body_acc_z"
  
  body_gyro_x_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/body_gyro_x_test.txt", header=F)
  #names(body_gyro_x_test) <- "body_gyro_x"
  body_gyro_y_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/body_gyro_y_test.txt", header=F)
  #names(body_gyro_y_test) <- "body_gyro_y"
  body_gyro_z_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/body_gyro_z_test.txt", header=F)
  #names(body_gyro_z_test) <- "body_gyro_z"
  
  total_acc_x_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/total_acc_x_test.txt", header=F)
  #names(total_acc_x_test) <- "total_acc_x"
  total_acc_y_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/total_acc_y_test.txt", header=F)
  #names(total_acc_y_test) <- "total_acc_y"
  total_acc_z_test <- read.table("./data/UCI HAR Dataset/test/Inertial Signals/total_acc_z_test.txt", header=F)
  #names(total_acc_z_test) <- "total_acc_z"
  
  print("Loading Test data. [DONE]")
  
  # Load Train
  print("Loading Train data...")
  subject_train <- read.csv("./data/UCI HAR Dataset/train/subject_train.txt", header=F)
  names(subject_train) <- "subject"
  
  X_train <- read.table("./data/UCI HAR Dataset/train/X_train.txt", header=F)
  names(X_train) <- features$V2
  y_train <- read.csv("./data/UCI HAR Dataset/train/y_train.txt", header=F)
  names(y_train) <- "y"
  
  body_acc_x_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/body_acc_x_train.txt", header=F)
  #names(body_acc_x_train) <- "body_acc_x"
  body_acc_y_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/body_acc_y_train.txt", header=F)
  #names(body_acc_y_train) <- "body_acc_y"
  body_acc_z_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/body_acc_z_train.txt", header=F)
  #names(body_acc_z_train) <- "body_acc_z"
  
  body_gyro_x_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/body_gyro_x_train.txt", header=F)
  #names(body_gyro_x_train) <- "body_gyro_x"
  body_gyro_y_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/body_gyro_y_train.txt", header=F)
  #names(body_gyro_y_train) <- "body_gyro_y"
  body_gyro_z_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/body_gyro_z_train.txt", header=F)
  #names(body_gyro_z_train) <- "body_gyro_z"
  
  total_acc_x_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/total_acc_x_train.txt", header=F)
  #names(total_acc_x_train) <- "total_acc_x"
  total_acc_y_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/total_acc_y_train.txt", header=F)
  #names(total_acc_y_train) <- "total_acc_y"
  total_acc_z_train <- read.table("./data/UCI HAR Dataset/train/Inertial Signals/total_acc_z_train.txt", header=F)
  #names(total_acc_z_train) <- "total_acc_z"
  
  print("Loading Train data. [DONE]")
  
  # Combine Test & Train
  
  print("==================================================")
  print("=                SIMPLE DEBUG TREE               =")
  print("==================================================")
  
  watch("Features", features)
  watch("Activity Labels", activity_labels)
  
  subject <- data.frame()
  subject <- rbind(subject, subject_test)
  subject <- rbind(subject, subject_train)
  watch("Subject", subject)
  
  X <- data.frame()
  X <- rbind(X, X_test)
  X <- rbind(X, X_train)
  watch("X", X)
  #colnames(X) <- c(features[2])
  
  #print("-------------------------------------------------------------------")
  #print(names(X))
  #print("-------------------------------------------------------------------")
  
  y <- data.frame()
  y <- rbind(y, y_test)
  y <- rbind(y, y_train)
  watch("y", y)
  
  body_acc_x <- data.frame()
  body_acc_x <- rbind(body_acc_x, body_acc_x_test)
  body_acc_x <- rbind(body_acc_x, body_acc_x_train)
  watch("body_acc_x", body_acc_x)
  
  body_acc_y <- data.frame()
  body_acc_y <- rbind(body_acc_y, body_acc_y_test)
  body_acc_y <- rbind(body_acc_y, body_acc_y_train)
  watch("body_acc_y", body_acc_y)
  
  body_acc_z <- data.frame()
  body_acc_z <- rbind(body_acc_z, body_acc_z_test)
  body_acc_z <- rbind(body_acc_z, body_acc_z_train)
  watch("body_acc_z", body_acc_z)
  
  body_gyro_x <- data.frame()
  body_gyro_x <- rbind(body_gyro_x, body_gyro_x_test)
  body_gyro_x <- rbind(body_gyro_x, body_gyro_x_train)
  watch("body_gyro_x", body_gyro_x)
  
  body_gyro_y <- data.frame()
  body_gyro_y <- rbind(body_gyro_y, body_gyro_y_test)
  body_gyro_y <- rbind(body_gyro_y, body_gyro_y_train)
  watch("body_gyro_y", body_gyro_y)
  
  body_gyro_z <- data.frame()
  body_gyro_z <- rbind(body_gyro_z, body_gyro_z_test)
  body_gyro_z <- rbind(body_gyro_z, body_gyro_z_train)
  watch("body_gyro_z", body_gyro_z)
  
  total_acc_x <- data.frame()
  total_acc_x <- rbind(total_acc_x, total_acc_x_test)
  total_acc_x <- rbind(total_acc_x, total_acc_x_train)
  watch("total_acc_x", total_acc_x)
  
  total_acc_y <- data.frame()
  total_acc_y <- rbind(total_acc_y, total_acc_y_test)
  total_acc_y <- rbind(total_acc_y, total_acc_y_train)
  watch("total_acc_y", total_acc_y)
  
  total_acc_z <- data.frame()
  total_acc_z <- rbind(total_acc_z, total_acc_z_test)
  total_acc_z <- rbind(total_acc_z, total_acc_z_train)
  watch("total_acc_z", total_acc_z)
  
  print("==================================================")
  
  # Clean Data
  
  # Merge Data
  print("Merging all data...")
  y <- merge(activity_labels, y, by.x="id", by.y="y", all=F)$name
  
  data <- data.frame(y)

  data <- cbind(data, X)
  data <- cbind(data, subject)
  
  if(0){
    data <- cbind(data, body_acc_x)
    data <- cbind(data, body_acc_y)
    data <- cbind(data, body_acc_z)
    data <- cbind(data, body_gyro_x)
    data <- cbind(data, body_gyro_y)
    data <- cbind(data, body_gyro_z)
    data <- cbind(data, total_acc_x)
    data <- cbind(data, total_acc_y)
    data <- cbind(data, total_acc_z)  
  }
  
  print("Merging all data. [DONE]")
  
  #head(data, 3)
  
  # Calculate Mean
  print("Calculating Mean...")
  print(summary(data))
  print("Calculating Mean. [DONE]")
  
  # Calculate Standard Deviation
  
  print("Calculating Standard Deviation...")
  print(lapply(data, sd))
  print("Calculating Standard Deviation. [DONE]")
  
  print("Saving Result to (./data/tidyData.csv)..." )
  write.csv(data, "./data/tidyData.csv")
  print("Saving Result to (./data/tidyData.csv). [DONE]" )
  
  print("####################################")
  print("#####   PROJECT SOLUTION DONE  #####")
  print("####################################")
  
  return(data)
}

```

## License
Anything here is for Educational purpose only, done at 25 April 2014.