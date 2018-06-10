---
title: "MKuklani_homework5_assignment"
author: "Mahesh Kuklani"
date: "June 7, 2018"
output: 
  html_document:
    keep_md: true
---



## 1.	Data Munging (30 points): Utilize yob2016.txt for this question. This file is a series of popular children's names born in the year 2016 in the United States.  It consists of three columns with a first name, a gender, and the amount of children given that name.  However, the data is raw and will need cleaning to make it tidy and usable.  
### a.	First, import the .txt file into R so you can process it.  Keep in mind this is not a CSV file.  You might have to open the file to see what you're dealing with.  Assign the resulting data frame to an object, df, that consists of three columns with human-readable column names for each.   
### b.	Display the summary and structure of df  


```r
#set working directory

setwd("E:/Mahesh/SMU/MSDS6306 Doing Data Science/DataSets")

# read the text file

df <- read.table("yob2016.txt", sep = ";")

# set the column names to name, gender and children
colnames(df) <- c("name", "gender", "children")

head(df)
```

```
##       name gender children
## 1     Emma      F    19414
## 2   Olivia      F    19246
## 3      Ava      F    16237
## 4   Sophia      F    16070
## 5 Isabella      F    14722
## 6      Mia      F    14366
```

```r
# no of rows in the dataset
nrow(df)
```

```
## [1] 32869
```

## c.	Your client tells you that there is a problem with the raw file.  One name was entered twice and misspelled.  The client cannot remember which name it is; there are thousands he saw! But he did mention he accidentally put three y's at the end of the name.  Write an R command to figure out which name it is and display it.  

## d.	Upon finding the misspelled name, please remove this particular observation, as the client says it's redundant.  Save the remaining dataset as an object: y2016  


```r
# find the name ending with 3y's
name.with.3ys <- grep("yyy$", df$name, value=TRUE)
name.with.3ys
```

```
## [1] "Fionayyy"
```

```r
# get the record number of the name with 3y's
name.with.3ys <- grep("yyy$", df$name)
name.with.3ys
```

```
## [1] 212
```

```r
# delete the record with 3y's
y2016 <- df[-212,]

# no of rows in the dataset after removing record with 3y's
nrow(y2016)
```

```
## [1] 32868
```
## 2.	Data Merging (30 points): Utilize yob2015.txt for this question.  This file is similar to yob2016, but contains names, gender, and total children given that name for the year 2015.  
## a.	Like 1a, please import the .txt file into R.  Look at the file before you do.  You might have to change some options to import it properly.  Again, please give the dataframe human-readable column names.  Assign the dataframe to y2015.  
## b.	Display the last ten rows in the dataframe.  Describe something you find interesting about these 10 rows.  
## c.	Merge y2016 and y2015 by your Name column; assign it to final.  The client only cares about names that have data for both 2016 and 2015; there should be no NA values in either of your amount of children rows after merging.  


```r
#set working directory
setwd("E:/Mahesh/SMU/MSDS6306 Doing Data Science/DataSets")

# read the text file
df.2015 <- read.table("yob2015.txt", sep = ",")

# set the column names to name, gender and children
colnames(df.2015) <- c("name", "gender", "children")

head(df.2015)
```

```
##       name gender children
## 1     Emma      F    20415
## 2   Olivia      F    19638
## 3   Sophia      F    17381
## 4      Ava      F    16340
## 5 Isabella      F    15574
## 6      Mia      F    14871
```

```r
# display last 10 rows of this dataset

tail(df.2015, 10)
```

```
##         name gender children
## 33054   Ziyu      M        5
## 33055   Zoel      M        5
## 33056  Zohar      M        5
## 33057 Zolton      M        5
## 33058   Zyah      M        5
## 33059 Zykell      M        5
## 33060 Zyking      M        5
## 33061  Zykir      M        5
## 33062  Zyrus      M        5
## 33063   Zyus      M        5
```

```r
## All these names are rare and are for male gender

#Merge the dataset based on name and gender
final <- merge(df, df.2015, by=c("name", "gender"))

#check if there are any na values in the merge

which(!complete.cases(final)) ## gives whether there are NA's in the dataset
```

```
## integer(0)
```

## 3.	Data Summary (30 points): Utilize your data frame object final for this part.  
## a.	Create a new column called "Total" in final that adds the amount of children in 2015 and 2016 together.  In those two years combined, how many people were given popular names?  
## b.	Sort the data by Total.  What are the top 10 most popular names?  
## c.	The client is expecting a girl!  Omit boys and give the top 10 most popular girl's names.  
## d.	Write these top 10 girl names and their Totals to a CSV file.  Leave out the other columns entirely.  


```r
final$total <- final$children.x + final$children.y

# people given popular names
sum(final$total)
```

```
## [1] 7239231
```

```r
# sort the data by total
final.total.sort <- final[order(-final$total),]

# 10 most popular names
popular.names <- head(final.total.sort, 10)
popular.names[,1]
```

```
##  [1] Emma     Olivia   Noah     Liam     Sophia   Ava      Mason   
##  [8] William  Jacob    Isabella
## 30295 Levels: Aaban Aabha Aabid Aabir Aabriella Aadam Aadarsh ... Zyva
```

```r
# omit boys
final.girl <- subset(final, gender=="F")

# sort this in descending order of popular names
final.girl.sort <- final.girl[order(-final.girl$total),]

# 10 most popular girl's names
popular.girls.names <- head(final.girl.sort, 10)
popular.girls.names[,1]
```

```
##  [1] Emma      Olivia    Sophia    Ava       Isabella  Mia       Charlotte
##  [8] Abigail   Emily     Harper   
## 30295 Levels: Aaban Aabha Aabid Aabir Aabriella Aadam Aadarsh ... Zyva
```

```r
# write it to a csv file
write.csv(popular.girls.names[,1], file="E:/Mahesh/SMU/MSDS6306 Doing Data Science/Homework/5/popular_girls_names.csv", row.names=FALSE)
```
