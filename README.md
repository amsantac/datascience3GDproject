#Course project for Data Science - Getting and Cleaning Data
 
This script starts with the assumption that the Samsung data is available in the working directory in an unzipped UCI HAR Dataset folder


###1. Merge the training and the test sets to create one data set

Read the features file
```{r}
features <- read.table("features.txt")
```

Read the subject and activity test datasets and provide column names
```{r}
subject_test <- read.table("test/subject_test.txt")
colnames(subject_test) <- "Subject"
y_test <- read.table("test/y_test.txt")
colnames(y_test) <- "Activity"
```

Read the subject and activity training datasets and provide column names
```{r}
subject_train <- read.table("train/subject_train.txt")
colnames(subject_train) <- "Subject"
y_train <- read.table("train/y_train.txt")
colnames(y_train) <- "Activity"
```

Read the test and training sets
```{r}
x_test <- read.table("test/x_test.txt")
colnames(x_test) <- features[, 2]
x_train <- read.table("train/x_train.txt")
colnames(x_train) <- features[, 2]
```

Row bind the test and training sets
```{r}
values <- rbind(x_test, x_train)
```

###2. Extracts only the measurements on the mean and standard deviation for each measurement in the values dataset

Identify the column names of variables corresponding to mean and standard deviation for each measurement

```{r}
colvalues_mean <- grep("-mean()", colnames(values), fixed=TRUE)
colvalues_std <- grep("-std()", colnames(values), fixed=TRUE)
```

Extract the selected variables
```{r}
values2 <- values[, c(colvalues_mean, colvalues_std)]
```

Row bind subject test and training sets
```{r}
subject <- rbind(subject_test, subject_train)
```

Row bind activity test and training sets
```{r}
activity <- rbind(y_test, y_train)
```

Column bind subject set, activity set and values set
```{r}
dataset <- cbind(values2, subject, activity)
```

###3. Uses descriptive activity names to name the activities in the data se

Read the activity labels file
```{r}
labels <- read.table("activity_labels.txt")
```

Merge the dataset with the activity labels set and rename the activity columns
```{r}
dataset <- merge(dataset, labels, by.x="Activity", by.y="V1")
dataset <- dataset[, -1]

library(dplyr)
dataset <- rename(dataset, Activity=V2)
```

###4. create a second, independent tidy data set with the average of each variable for each activity and each subject.

First, tidy the data in the long-tidy form
```{r}
library(tidy)
dataset2 <- gather(dataset, Measurement, Value, -c(Subject, Activity))
```

Group the dataset by Subject, Activity and Measurement 
```{r}
dataset3 <- group_by(dataset2, Subject, Activity, Measurement)
```

Calculate the average of each variable for each activity and each subject
```{r}
dataset4 <- summarize(dataset3, Average=mean(Value))
```

Finally, export the dataset
```{r}
write.table(dataset4, "tidyDataset.txt", row.name=FALSE)
```
