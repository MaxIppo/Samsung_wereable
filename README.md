
## SAMSUNG WEREABLE PROJECT: DELIVER A TIDY DATA SET FOR FURTHER ANALYSIS
# The process for delivering SAMSUNG WEREABLE TIDY DATA SET starts from a raw data environment sit in UCI MLR
# The process follow some steps:
# 1) Download the .zip data
on the local PC, in a subdirectory of the working directory (i.e. "./run_analysis")
# 2) Extract .zip file 
in a specific directory structure, where the data are split based on purpose (i.e. training and test)

#Dowload .zip File
setwd("D:/DATA_SCIENCE/Get_the_Data/week_3_project")
fileUrl<-"https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
mainDir <- getwd()
subDir <- "run_analysis"
if (!file.exists(subDir)) {dir.create(file.path(mainDir, subDir))}
zipFile<-"./run_analysis/run_analysis.zip"
download.file(fileUrl,zipFile, method="libcurl", mode = "wb")
unzip(zipFile, exdir = "./run_analysis/data")


#Read Training Data Sets: 'train/X_train.txt': Training set.
train_ds_x <- read.table("./run_analysis/data/UCI HAR Dataset/train/X_train.txt", quote="\"", comment.char="")
train_subject <- read.table("./run_analysis/data/UCI HAR Dataset/train/subject_train.txt", quote="\"", comment.char="")
train_activities_y <- read.table("./run_analysis/data/UCI HAR Dataset/train/y_train.txt", quote="\"", comment.char="")

#Read Test Data Sets: 'test/X_test.txt': Test set.
test_ds_x <- read.table("./run_analysis/data/UCI HAR Dataset/test/X_test.txt", quote="\"", comment.char="")
test_subject <- read.table("./run_analysis/data/UCI HAR Dataset/test/subject_test.txt", quote="\"", comment.char="")
test_activities_y <- read.table("./run_analysis/data/UCI HAR Dataset/test/y_test.txt", quote="\"", comment.char="")


#Merges the training and the test sets to create one data set
uniqueDs<-rbind(train_ds_x, test_ds_x)
uniqueSubject<-rbind(train_subject, test_subject)
uniqueActivities_y<-rbind(train_activities_y, test_activities_y)

# Extracts only the measurements on the mean and standard deviation for each measurement. 
features <- read.table("./run_analysis/data/UCI HAR Dataset/features.txt", quote="\"", comment.char="")
featuresVector<-as.vector(features[,2])
sub_index_col <- vector("logical", length = length(featuresVector))
for(i in 1:length(name_vect)) {
        sub_index_col[i]=(grepl("mean", featuresVector[i], perl=TRUE) | grepl("std", featuresVector[i], perl=TRUE))
        }
tinyUniqueDs<-subset(uniqueDs,select=sub_index_col)
tinyUniqueDs<-cbind(uniqueSubject, uniqueActivities_y, tinyUniqueDs)


# Assign labels to the data set to make it easier column selection

nameVector_A<-"Subject"
nameVector_B<-"Activity"
nameVector_C<-featuresVector[sub_index_col]
nameVector<-c (nameVector_A,nameVector_B, nameVector_C)
names(tinyUniqueDs)<-nameVector

for(i in 1:length(tinyUniqueDs$Activity)) {
        if(tinyUniqueDs$Activity[i]==1) {tinyUniqueDs$Activity[i]<- "WALKING"}
        else
        if(tinyUniqueDs$Activity[i]==2) {tinyUniqueDs$Activity[i]<- "WALKING_UPSTAIRS"}
        else
        if(tinyUniqueDs$Activity[i]==3) {tinyUniqueDs$Activity[i]<- "WALKING_DOWNSTAIRS"}
        else
        if(tinyUniqueDs$Activity[i]==4) {tinyUniqueDs$Activity[i]<- "SITTING"}
        else
        if(tinyUniqueDs$Activity[i]==5) {tinyUniqueDs$Activity[i]<- "STANDING"}
        else
        if(tinyUniqueDs$Activity[i]==6) {tinyUniqueDs$Activity[i]<- "LAYING"}
        else
        print ("Attività non prevista")        
        }
tinyUniqueDs$Subject<-as.factor(tinyUniqueDs$Subject)
tinyUniqueDs$Activity<-as.factor(tinyUniqueDs$Activity)

# Appropriately labels the data set with descriptive variable names. 

#From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
names<-names(tinyUniqueDs)
s<-list(tinyUniqueDs$Subject,tinyUniqueDs$Activity)# list of factors of the 2 slection colums
splitDs<-split(tinyUniqueDs,s)
splitSet<-sapply(splitDs, function(x) {
        colMeans(x[, shortNames])
})

Deliverable<-t(splitSet)
out <- file("./run_analysis/data/deliverable.txt", "w")
write.table(Deliverable, out, row.names = FALSE)
