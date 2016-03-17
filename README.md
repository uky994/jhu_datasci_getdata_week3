#Joey C's Getting and Cleaning Data Project for JHUs Data Science Course Track

##Description
You can find more information about the data set, variables, and transformations used in this project in the Getting and Cleaning Data course at John's Hopkins Univeristy.

##Data Source
A full description of the data used in this project can be found at [The UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)
The source data for this project can be found [here](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip).

##Data Set Information
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

###Attribute Information
For each record in the dataset it is provided: 
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

##Data Citation
Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. A Public Domain Dataset for Human Activity Recognition Using Smartphones. 21th European Symposium on Artificial Neural Networks, Computational Intelligence and Machine Learning, ESANN 2013. Bruges, Belgium 24-26 April 2013.

##File Information
The crux of this repository is inside run_analysis.R which does the following:
1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

###For each record it is provided
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

###The final dataset includes information from the following files
- 'features.txt': List of all features.
- 'activity_labels.txt': Links the class labels with their activity name.
- 'train/X_train.txt': Training set.
- 'train/y_train.txt': Training labels.
- 'train/subjects_train.txt' : A list of subjects in the training dataset
- 'test/X_test.txt': Test set.
- 'test/y_test.txt': Test labels.
- 'test/subjects_test.txt' : A list of all subjects in the test dataset

###The following files are available for the train and test data. Their descriptions are equivalent. 
- 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 
- 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity units 'g'. Every row shows a 128 element vector. The same description applies for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 
- 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total acceleration. 
- 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The units are radians/second. 
####Note: While the code reads in these files and renames their columns they are not included in the final dataset, but they can be in by modifying the rbind statement in line 197 of run_analysis.R


###Outline of run_analysis.R
1. Merge the training and the test sets to create one data set.
- set the source directory for the files, read into tables the data located in
-features.txt
-activity_labels.txt
-subject_train.txt
-x_train.txt
-y_train.txt
-subject_test.txt
-x_test.txt
-y_test.txt

2. Assign column names and merge to create one data set.
-use names() and assignments to rename columns
-column 2 of the features dataset correspond to the x_train and x_test column names

3. Extract only the measurements on the mean and standard deviation for each measurement.
-using grepl, identify names in features.txt that contain the mean and standard deviation measured for each feature. 
-subset the data to keep only the necessary columns.

4. Use descriptive activity names to name the activities in the data set
-merge data subset with the activity_labels.txt table to inlude the descriptive activity names

5. Appropriately label the data set with descriptive activity names.
-gsub function strips unnecessary characters and cleans up the data labels.

6. Create a second, independent tidy data set with the average of each variable for each activity and each subject.
-the aggregate function summarizes our data set with the average of each variable by activity and subject.