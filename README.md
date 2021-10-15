# Samsung1
Samsung_data_Getting&amp;cCeaning_data

Main steps in main run_analysis.R code:

Step 1   Merges the training and the test sets to create one data set
1.1_check dimensions of each set of training data dim()
1.2_check dimensions of each set of test data dim()
1.3_put data training together (cbind)
1.4_put data test together (cbind)
1.5_put data train and test together(rbind) (result:dataframe"all_data")
1.6 put diffrent working name for each column (names: V1:V12)



#2.Extracts only the measurement on the mean and standard diviation for each measurement
I start from building data frame from "X_train.txt" and "X_train.txt" with columns names from "features.txt", than using grep function I obtain new data frame (d_total) only with the measurement on the mean and standard diviation

new_df_feature<-data.frame(c(feature_label))
#nrow(new_df_feature)
#561
c_data_x_train<-read.csv("./UCI HAR Dataset/train/X_train.txt",header = FALSE,sep = "")
c_data_x_test<-read.csv("./UCI HAR Dataset/test/X_test.txt", header = FALSE,sep = "")
c_data_x_together<-rbind(c_data_x_train,c_data_x_test)
names(c_data_x_together)<-c(feature_label)
e<-grep("mean",new_df_feature$c.feature_label.)
#head(e)
#1 2 3 41 42 43
e1<-grep("std",new_df_feature$c.feature_label.)
#head(e1)
#4 5 6 44 45 46
d<-c_data_x_together[ ,e]
d1<-c_data_x_together[ ,e1]
d_total<-cbind(d,d1)
#in this dataframe you find only the measurement on the mean and standard diviation for each measurement

#3.Add descriptive activity names to name the activities in the data set
activity_labels<-read.csv("./UCI HAR Dataset/activity_labels.txt",header = FALSE)

all_data2<-mutate(all_data,activity=V3)

act_tabela<-mutate(activity_labels,activity_number=activity_labels)
names(act_tabela)<-c("act_number","act_name")
SplitText<-strsplit(act_tabela$act_number," ")
firstElement<-function(x){x[1]}
sapply(SplitText,firstElement)
tab_pom<-mutate(act_tabela,act_num=sapply(SplitText,firstElement))

all_data2<-merge(all_data, tab_pom, by.x = "V3",by.y ="act_num")
all_data3<-select(all_data2,V1:act_number)
#View(all_data3)


#4.Appropriately labels the data set with descriptive variable names
#names(all_data)<-c("piekna nazwa 1","piekna nazwa 2","V3","V4","V5","V6","V7","V8","V9","V10","V11","V12")
all_data3<-rename(all_data3,"subject_id"="V1","features"="V2","activity"="act_number","body_acc_x"="V4", "body_acc_y"="V5", "body_acc_z"="V6", "body_gyro_x"="V7", "body_gyro_y"="V8", "body_gyro_z"="V9", "total_acc_x"="V10", "total_acc_y"="V11", "total_acc_z"="V12")

#5.From the data set in step 4, create a second, independent tidy data set with the average of each variable for each activity and each subject
#5.1_Train data
c_body_acc_x_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/body_acc_x_train.txt",header = FALSE,sep = "")
c_body_acc_y_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/body_acc_y_train.txt",header = FALSE,sep = "")
c_body_acc_z_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/body_acc_z_train.txt",header = FALSE,sep = "")
c_body_gyro_x_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/body_gyro_x_train.txt",header = FALSE,sep = "")
c_body_gyro_y_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/body_gyro_y_train.txt",header = FALSE,sep = "")
c_body_gyro_z_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/body_gyro_z_train.txt",header = FALSE,sep = "")
c_total_acc_x_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/total_acc_x_train.txt",header = FALSE,sep = "")
c_total_acc_y_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/total_acc_y_train.txt",header = FALSE,sep = "")
c_total_acc_z_train<-read.csv("./UCI HAR Dataset/train/Inertial Signals/total_acc_z_train.txt",header = FALSE,sep = "")

#5.2_test data
c_body_acc_x_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/body_acc_x_test.txt",header = FALSE,sep = "")
c_body_acc_y_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/body_acc_y_test.txt",header = FALSE,sep = "")
c_body_acc_z_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/body_acc_z_test.txt",header = FALSE,sep = "")
c_body_gyro_x_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/body_gyro_x_test.txt",header = FALSE,sep = "")
c_body_gyro_y_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/body_gyro_y_test.txt",header = FALSE,sep = "")
c_body_gyro_z_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/body_gyro_z_test.txt",header = FALSE,sep = "")
c_total_acc_x_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/total_acc_x_test.txt",header = FALSE,sep = "")
c_total_acc_y_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/total_acc_y_test.txt",header = FALSE,sep = "")
c_total_acc_z_test<-read.csv("./UCI HAR Dataset/test/Inertial Signals/total_acc_z_test.txt",header = FALSE,sep = "")

#5.3_Mean calculation for each measurement and variable
f11<-mutate(c_body_acc_x_train,V129=rowMeans(c_body_acc_x_train))
g11<-select(f11,V129)
f12<-mutate(c_body_acc_y_train,V129=rowMeans(c_body_acc_y_train))
g12<-select(f12,V129)
f13<-mutate(c_body_acc_z_train,V129=rowMeans(c_body_acc_z_train))
g13<-select(f13,V129)
f14<-mutate(c_body_gyro_x_train,V129=rowMeans(c_body_gyro_x_train))
g14<-select(f14,V129)
f15<-mutate(c_body_gyro_y_train,V129=rowMeans(c_body_gyro_y_train))
g15<-select(f15,V129)
f16<-mutate(c_body_gyro_z_train,V129=rowMeans(c_body_gyro_z_train))
g16<-select(f16,V129)
f17<-mutate(c_total_acc_x_train,V129=rowMeans(c_total_acc_x_train))
g17<-select(f17,V129)
f18<-mutate(c_total_acc_y_train,V129=rowMeans(c_total_acc_y_train))
g18<-select(f18,V129)
f19<-mutate(c_total_acc_z_train,V129=rowMeans(c_total_acc_z_train))
g19<-select(f19,V129)

f21<-mutate(c_body_acc_x_test,V129=rowMeans(c_body_acc_x_test))
g21<-select(f21,V129)
f22<-mutate(c_body_acc_y_test,V129=rowMeans(c_body_acc_y_test))
g22<-select(f22,V129)
f23<-mutate(c_body_acc_z_test,V129=rowMeans(c_body_acc_z_test))
g23<-select(f23,V129)
f24<-mutate(c_body_gyro_x_test,V129=rowMeans(c_body_gyro_x_test))
g24<-select(f24,V129)
f25<-mutate(c_body_gyro_y_test,V129=rowMeans(c_body_gyro_y_test))
g25<-select(f25,V129)
f26<-mutate(c_body_gyro_z_test,V129=rowMeans(c_body_gyro_z_test))
g26<-select(f26,V129)
f27<-mutate(c_total_acc_x_test,V129=rowMeans(c_total_acc_x_test))
g27<-select(f27,V129)
f28<-mutate(c_total_acc_y_test,V129=rowMeans(c_total_acc_y_test))
g28<-select(f28,V129)
f29<-mutate(c_total_acc_z_test,V129=rowMeans(c_total_acc_z_test))
g29<-select(f29,V129)

#5.4_put all mean of training dta together
c_all_train_data<-cbind(data_subject_train,data_y_train,g11,g12,g13,g14,g15,g16,g17,g18,g19)

#5.4_put all mean of test data together
c_all_test_data<-cbind(data_subject_test,data_y_test,g21,g22,g23,g24,g25,g26,g27,g28,g29)

#5.5_put data train and test together
c_all_data<-rbind(c_all_train_data,c_all_test_data)

#5.51 put diffrent working name for each column
names(c_all_data)<-c("subject_id","activity_no","a_body_acc_x","a_body_acc_y","a_body_acc_z","a_body_gyro_x","a_body_gyro_y","a_body_gyro_z","a_total_acc_x","a_total_acc_y","a_total_acc_z")

#5.6 put descriptive activity names and column ordering
c_all_data_new<-merge(c_all_data, tab_pom, by.x = "activity_no",by.y ="act_num")
c_all_data_new1<-select(c_all_data_new,subject_id,activity=act_number,3:11)
# here you find second, independent tidy data set with the average of each variable for each activity and each subject
write.table(c_all_data_new1,file = "window_averages_data.txt", row.names = FALSE)
