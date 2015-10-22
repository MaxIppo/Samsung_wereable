
## SAMSUNG WEREABLE PROJECT: DELIVER A TIDY DATA SET FOR FURTHER ANALYSIS
#The process for delivering SAMSUNG WEREABLE TIDY DATA SET starts from a raw data environment sit in UCI MLR
# The process follow some steps:
# 1) Download the .zip data in the local PC;
a subdirectory of the working directory (i.e. "./run_analysis") is created where the .zip file is downloaded. The script cretaes the drectory if it wold not exist;
# 2) Extract .zip file;
The extraction process creates a subdirectory structure ".../UCI HAR Dataset/..." of the directory where the .zip fil is sit. in a specific directory structure, where the data are split based on "purpose" o f data (i.e. training and test). In each directory (i.e. training and test) there are 3 txt files; The following list describe training data files, symmetric naming is used for test files (i.e. prefix "test" is used instead of "training":  X_train.txt (represents for each row the data sampled; it is the core data set file), subject_train.txt (that identify the id of the Samsung device users, called "individuals"; each raw of the data set correspond only to one individual) , y_train.txt (describe the activity performed by each individual during each data sampling)
# 3) Upload raw data files in R;
Each data is uploaded in one specific Data Frame: 
train_ds_x <- X_train.txt
train_subject <- subject_train.txt
train_activities_y <- y_train.txt
test_ds_x <- X_test.txt
test_subject <- subject_test.txt
test_activities_y <- y_test.txt
# 4) Merge of training and test data set
Only core dataset (train_ds_x, test_ds_x) are merged (i.e. lines are appended, the number of columns obviuously corresponds in a unique dataset, to simplify df semplification
# 5) Selection of a subset of columns related to "mean" or "standard deviation" for each measureme
Column whose name name tracts only the measurements on the mean and standard deviation for each measurement. 
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
