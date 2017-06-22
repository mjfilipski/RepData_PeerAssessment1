# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
These are the libraries used to compile this code:

```r
library(knitr)
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
datazip <- "activity.zip"
datafile <- unzip(datazip)
d <- read.csv(datafile, header=TRUE)
```


## What is mean total number of steps taken per day?
1 - Here is a histogram of the steps taken each day 

```r
daily <- aggregate(steps ~ date, d,sum)
hist(daily$steps, main = "Histogram of total number of daily steps")
```

![](PA1_template_files/figure-html/dailyhist-1.png)<!-- -->

2 - Here is some code to calculate the mean and median

```r
msteps <- mean(daily$steps)
medsteps <- median(daily$steps)
```
The mean number of steps taken per day is 10766, and the median is 10765.  




## What is the average daily activity pattern?
1 - Here is a plot of the average number of steps in a given 5-minute interval

```r
mean_byint<-aggregate(steps ~ interval, d, mean)
plot(steps ~ interval, type="l", data=mean_byint)
```

![](PA1_template_files/figure-html/daily_patterns-1.png)<!-- -->
2 - Here we find out what the maximum interval is, and when it occurrs  


```r
max <- max(mean_byint$steps)
maxint <- filter(mean_byint, steps == max)[1,1]
maxhr <- floor(maxint/100) 
maxmin <- maxint-maxhr*100
```
The interval with maximum average number is of steps taken is the one starting at 8:35. The subject took 206.1698113 steps at that time of the day. 


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
