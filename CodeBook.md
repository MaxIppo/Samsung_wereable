## SAMSUNG WEREABLE PROJECT: DELIVER A TIDY DATA SET FOR FURTHER ANALYSIS


#The process for delivering SAMSUNG WEREABLE TIDY DATA SET starts from a raw data environment sit in UCI MLR

# The data transformation process follows some steps:

# 1) Download the .zip data in the local PC

a subdirectory of the working directory (i.e. "./run_analysis") is created where the .zip file is downloaded. The script cretaes the drectory if it wold not exist;

# 2) Extract .zip file

The extraction process creates a subdirectory structure ".../UCI HAR Dataset/..." of the directory where the .zip fil is sit. in a specific directory structure, where the data are split based on "purpose" o f data (i.e. training and test). In each directory (i.e. training and test) there are 3 txt files; The following list describe training data files, symmetric naming is used for test files (i.e. prefix "test" is used instead of "training":  X_train.txt (represents for each row the data sampled; it is the core data set file), subject_train.txt (that identify the id of the Samsung device users, called "individuals"; each raw of the data set correspond only to one individual) , y_train.txt (describe the activity performed by each individual during each data sampling)
# 3) Upload raw data files in R
Each data is uploaded in one specific Data Frame: 
train_ds_x <- X_train.txt
train_subject <- subject_train.txt
train_activities_y <- y_train.txt
test_ds_x <- X_test.txt
test_subject <- subject_test.txt
test_activities_y <- y_test.txt

# 4) Merge of training and test data set

Only core dataset (train_ds_x, test_ds_x) are merged (i.e. lines are appended, the number of columns obviuously corresponds in a unique dataset, to simplify df semplification

# 5) Selection of a subset of columns related to "mean" or "standard deviation" for each measurement

Logical vector technique has been used for selecting the names of measurements containing "mean" or "std" and therefore to subset the identified columns. 
The resulting Datast has been bound with the columns identifying individuals and activities for each measurement 

# 6) Assign labels to the data set

Subject and activity variables have been named with specific meaningful strings ("Subject" and "Activity"), columns related to the indicators has been named with the name provided in the file "features" wheose subset has bee identified when the columns relted to "mean" or "standard deviation" measurement. Both Activity and Subject colums have bee transformed in factors. 

# 7) Subsed a tidy data set  with the average of each variable for each activity and each subject.

The function split has been used and the "Activity" and "Subject" factors have been leveraged as a list, to subset the "tinyUniqueDs" Dataset. Once split the sappy function have been applied with the function "Mean" for each dataset got ftom split function. The final tidy dataset has been named "Deliverable"

# 8) Issue the file as a .txt file

After opening a file channel, the file has been issued as deliverable.txt in the directory "./run_analysis/data/deliverable.txt".








# Variable Description

tBodyAcc-mean()-X -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Time domain 
tBodyAcc-mean()-Y -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Time domain 
tBodyAcc-mean()-Z -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Time domain 
tBodyAcc-std()-X -> Measure of  the Standard Deviation Of Acceleration due to Body movement  in the Time domain 
tBodyAcc-std()-Y -> Measure of  the Standard Deviation Of Acceleration due to Body movement  in the Time domain 
tBodyAcc-std()-Z -> Measure of  the Standard Deviation Of Acceleration due to Body movement  in the Time domain 
tGravityAcc-mean()-X -> Measure of  the Mean Value Of Acceleration due to Gravity  in the Time domain 
tGravityAcc-mean()-Y -> Measure of  the Mean Value Of Acceleration due to Gravity  in the Time domain 
tGravityAcc-mean()-Z -> Measure of  the Mean Value Of Acceleration due to Gravity  in the Time domain 
tGravityAcc-std()-X -> Measure of  the Standard Deviation Of Acceleration due to Gravity  in the Time domain 
tGravityAcc-std()-Y -> Measure of  the Standard Deviation Of Acceleration due to Gravity  in the Time domain 
tGravityAcc-std()-Z -> Measure of  the Standard Deviation Of Acceleration due to Gravity  in the Time domain 
tBodyAccJerk-mean()-X -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyAccJerk-mean()-Y -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyAccJerk-mean()-Z -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyAccJerk-std()-X -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyAccJerk-std()-Y -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyAccJerk-std()-Z -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyGyro-mean()-X -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Time domain 
tBodyGyro-mean()-Y -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Time domain 
tBodyGyro-mean()-Z -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Time domain 
tBodyGyro-std()-X -> Measure of  the Standard Deviation Of Angular Speed due to Body movement  in the Time domain 
tBodyGyro-std()-Y -> Measure of  the Standard Deviation Of Angular Speed due to Body movement  in the Time domain 
tBodyGyro-std()-Z -> Measure of  the Standard Deviation Of Angular Speed due to Body movement  in the Time domain 
tBodyGyroJerk-mean()-X -> Measure of  the Mean Value Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyGyroJerk-mean()-Y -> Measure of  the Mean Value Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyGyroJerk-mean()-Z -> Measure of  the Mean Value Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyGyroJerk-std()-X -> Measure of  the Standard Deviation Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyGyroJerk-std()-Y -> Measure of  the Standard Deviation Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyGyroJerk-std()-Z -> Measure of  the Standard Deviation Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyAccMag-mean() -> Measure of  the Mean Value Of Acceleration due to Body movement as Magnitude in the Time domain 
tBodyAccMag-std() -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Magnitude in the Time domain 
tGravityAccMag-mean() -> Measure of  the Mean Value Of Acceleration due to Gravity as Magnitude in the Time domain 
tGravityAccMag-std() -> Measure of  the Standard Deviation Of Acceleration due to Gravity as Magnitude in the Time domain 
tBodyAccJerkMag-mean() -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyAccJerkMag-std() -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Time domain 
tBodyGyroMag-mean() -> Measure of  the Mean Value Of Angular Speed due to Body movement as Magnitude in the Time domain 
tBodyGyroMag-std() -> Measure of  the Standard Deviation Of Angular Speed due to Body movement as Magnitude in the Time domain 
tBodyGyroJerkMag-mean() -> Measure of  the Mean Value Of Angular Speed due to Body movement as Jerked signal in the Time domain 
tBodyGyroJerkMag-std() -> Measure of  the Standard Deviation Of Angular Speed due to Body movement as Jerked signal in the Time domain 
fBodyAcc-mean()-X -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-mean()-Y -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-mean()-Z -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-std()-X -> Measure of  the Standard Deviation Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-std()-Y -> Measure of  the Standard Deviation Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-std()-Z -> Measure of  the Standard Deviation Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-meanFreq()-X -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-meanFreq()-Y -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Frequency domain 
fBodyAcc-meanFreq()-Z -> Measure of  the Mean Value Of Acceleration due to Body movement  in the Frequency domain 
fBodyAccJerk-mean()-X -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-mean()-Y -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-mean()-Z -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-std()-X -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-std()-Y -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-std()-Z -> Measure of  the Standard Deviation Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-meanFreq()-X -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-meanFreq()-Y -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyAccJerk-meanFreq()-Z -> Measure of  the Mean Value Of Acceleration due to Body movement as Jerked signal in the Frequency domain 
fBodyGyro-mean()-X -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-mean()-Y -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-mean()-Z -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-std()-X -> Measure of  the Standard Deviation Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-std()-Y -> Measure of  the Standard Deviation Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-std()-Z -> Measure of  the Standard Deviation Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-meanFreq()-X -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-meanFreq()-Y -> Measure of  the Mean Value Of Angular Speed due to Body movement  in the Frequency domain 
fBodyGyro-meanFreq()-Z -> Measure of  the Mean Value Of Angular Speed due to Body moveme


