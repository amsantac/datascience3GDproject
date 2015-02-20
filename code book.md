### Code book for the tidy dataset created with run_analysis.R
 
##1. Information about the variables

The tidy dataset created with the run_analysis.R code includes four variables: Subject, Activity, Measurement and Average.

#1. Subject: 
Each row identifies the subject who performed each activity that was measured. Its range is from 1 to 30 (integer values). The units of this variable correspond to individuals

#2. Activity: 
It corresponds to one out of six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) performed by each subject wearing a smartphone (Samsung Galaxy S II) on the waist. The units of this variable correspond to categories associated to the activities listed above

#3. Measurement: 
It corresponds to each of the features (66 in total) that were measured during the experiment for each of the activities performed by the subjects. For the tidy dataset, only the measurements on the mean and standard deviation for each measurement were extracted. The units of this variable correspond to categories related to the measurements provided

#4. Average: 
This column shows the average of each variable for each activity and each subject. The units for each observation is given in the same units as the variables in the original dataset as described in the README file in the UCI HAR Dataset folder

===========

A full description of the data collected from the accelerometers from the Samsung Galaxy S smartphone for this experiment is available at the site where the data was obtained: 

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The data used for this project was provided in the getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip file
