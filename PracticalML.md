First load the data file and extract all available data from the original data frame.


```r
df = read.csv('pml-training.csv');
df1 = df[,c('roll_belt','pitch_belt','yaw_belt','total_accel_belt','gyros_belt_x','gyros_belt_y','gyros_belt_z','accel_belt_x','accel_belt_y','accel_belt_z','magnet_belt_x','magnet_belt_y','magnet_belt_z','roll_arm','pitch_arm','yaw_arm','total_accel_arm','gyros_arm_x','gyros_arm_y','gyros_arm_z','accel_arm_x','accel_arm_y','accel_arm_z','magnet_arm_x','magnet_arm_y','magnet_arm_z','roll_dumbbell','pitch_dumbbell','yaw_dumbbell','total_accel_dumbbell','gyros_dumbbell_x','gyros_dumbbell_y','gyros_dumbbell_z','accel_dumbbell_x','accel_dumbbell_y','accel_dumbbell_z','magnet_dumbbell_x','magnet_dumbbell_y','magnet_dumbbell_z','roll_forearm','pitch_forearm','yaw_forearm','total_accel_forearm','gyros_forearm_x','gyros_forearm_y','gyros_forearm_z','accel_forearm_x','accel_forearm_y','accel_forearm_z','magnet_forearm_x','magnet_forearm_y','magnet_forearm_z','classe')];
```

Split the extracted data into training data and testing data.


```r
library(caret);
```

```
## Loading required package: lattice
## Loading required package: ggplot2
```

```r
inTrain <- createDataPartition(y=df1$classe,p = 0.6, list = FALSE);

training <- df1[inTrain,];
testing <- df1[-inTrain,];
```


Use random forest to train the data and obtain the predicting model.


```r
library(randomForest);
```

```
## randomForest 4.6-7
## Type rfNews() to see new features/changes/bug fixes.
```

```r
model.rf <- randomForest(classe~.,data= training)
```


Use testing data for predicting and plot the result.


```r
pre.rf <- predict(model.rf ,testing)
plot(pre.rf==testing$classe)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

