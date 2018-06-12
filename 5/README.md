This is readme for homework 5 

For this homework we had 2 dataset yob2015.txt which is a comma seperated file and yob2016.txt which is a ";" delimited file.

These files contain the popular baby names. We have to read file yob2016.txt and remove the name that has been misspelled with 3y's at the end.

Once data is tidy we have to read in the other file yob2015.txt and merge these 2 files. After merging the files we have to do a total of all baby names.

From the total count we have to find out the 10 most popular names and then 10 most popular girl names and store this information in .csv file.

Modified file .RMD with some changes.

-- How does the code work
1) Load file yob2016.txt in Dataset folder in a dataframe called df.
2) Give colnames as name, gender and children to this dataframe.
3) Display summary and structure of dataframe df
4) One of the names is duplicate and contains 3y's so remove this name
5) Read the file yob2015.txt into dataframe y2015
6) Set the columnames of this dataframe to names, gender and children
7) display last 10 records from dataframe y2015
8) Merge dataframes y2015 and df and create a new dataset called final
9) Remove all records that contain NA from final
10) Create a column called total that add the children with same names in children.x and children.y column.
11) Sort the dataframe based on total children
12) Give the total number of children that have popular names
13) Display 10 most popular names from the final dataset
14) From final dataset get names of girl child only
15) Show the 10 popular girls names
16) Write the 10 popular girls names to a csv file.
