
## SAMSUNG WEREABLE PROJECT -  DELIVER A TIDY DATA SET FOR FURTHER ANALYSIS
#This Repo contains:
#- run_analysis.R as an R Script
#- CodeBook.md as the codebook that describes the variables used in the tidy data-set, the data and transformations performed to clean up the data

#The script is aimed to clean-up raw data taken from wereable device and to structure a tidy data set that can be used for further analysis


#In order to better exploit the script please consider that:
#1) It downloads a .zip data in a local subdirectory of the working directory (i.e. "./run_analysis"),that is created if it wold not exist;
#2) It extracts the .zip filein a subdirectory structure ".../UCI HAR Dataset/..." of the directory where the .zip fil sits.
#3) It uploads raw data files 
#4) Merge training and test data set
#5) Select a subset of columns related to "mean" or "standard deviation" for each measurement
#6) Assign labels to the data set
#7) Subsed a tidy data set  with the average of each variable for each activity and each subject
#8) Issue the tidy data set file as a .txt file in the directory "./run_analysis/data/deliverable.txt".
