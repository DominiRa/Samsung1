# Samsung1
Samsung_data_Getting&amp;cCeaning_data



=================
Main steps in my run_analysis.R code:
=================


Step 1   Merges the training and the test sets to create one data set

1.1_check dimensions of each set of training data dim()

1.2_check dimensions of each set of test data dim()

1.3_put data training together (cbind)

1.4_put data test together (cbind)

1.5_put data train and test together(rbind) (result:dataframe"all_data")

1.6 put diffrent working name for each column (names: V1:V12)




======
Step 2  Extracts only the measurement on the mean and standard diviation for each measurement

I start from building data frame from "X_train.txt" and "X_train.txt" with columns names from "features.txt", than using grep function I obtain new data frame (d_total) only with the measurement on the mean and standard diviation



======
Step 3  Add descriptive activity names to name the activities in the data set

I start from reading "activity_labels.txt", then I create additional table with "activity dictionary" at the end I have dateframe (all_data3) with activity name (instead of activity number)



======
Step 4  Appropriately labels the data set with descriptive variable names

I use rename function to change variables' names (all_data3)



======
Step 5  Create a second, independent tidy data set with the average of each variable for each activity and each subject
I calculate the mean of 128 readings for each window, now I have only one "value" for each subject for each activity and each variable
I change CodeBook


======
Step 6 Write table
write.table(c_all_data_new1,file = "window_averages_data.txt", row.names = FALSE)
