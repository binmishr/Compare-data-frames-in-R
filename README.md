# Compare-data-frames-in-R

Compare data frames in R, In this tutorial we are going to describe how to compare data frames in R.

Let’s create a data frame

data1 <- data.frame(x1 = 1:5,            
                    x2 = LETTERS[1:5])
data2 <- data.frame(x1 = 1:5,
                    x2 = LETTERS[1:5])
data3 <- data.frame(x1 = 3:7,
                    x2 = LETTERS[1:5])

In the above data frame data1 and data2 are exactly same and data3 is completely different from other data sets.
Let’s install dplyr package for the function all_equal

install.packages("dplyr")               
library("dplyr")   

Example 1: Compare Equal Data Frames

Case1:-

In the first case, we’ll compare the first two data sets ie) data1 and data2. Based on all_equal function we can check whether the two data frames are equal or not.

all_equal(data1, data2)   
[1] TRUE 

Now you can see the function returned as TRUE, indicates both data sets are equal.

QQ-plots in R: Quantile-Quantile Plots-Quick Start Guide »

Case2:-

Now we can try comparedf function from library arsenal.

By default, the data frames are compared by row-by-row. You can change this using the by= or by.x= and by.y= arguments:

summary(compare(df1, df2))
summary(compare(df1, df2, by = "id"))
summary(compare(df1, df2, by = "row.names"))
library(arsenal)
comparedf(data1, data2)

Compare Object

Function Call: 
comparedf(x = data1, y = data2)
 Shared: 2 non-by variables and 5 observations.
Not shared: 0 variables and 0 observations.
 
Differences found in 0/2 variables compared.
0 variables compared have non-identical attributes.
summary(comparedf(data1, data2))
 Table: Summary of data.frames
 version   arg      ncol   nrow
--------  ------  -----  -----
x         data1       2      5
y         data2       2      5
Table: Summary of overall comparison
statistic                                                      value
------------------------------------------------------------  ------
Number of by-variables                                             0
Number of non-by variables in common                               2
Number of variables compared                                       2
Number of variables in x but not y                                 0
Number of variables in y but not x                                 0
Number of variables compared with some values unequal              0
Number of variables compared with all values equal                 2
Number of observations in common                                   5
Number of observations in x but not y                              0
Number of observations in y but not x                              0
Number of observations with some compared variables unequal        0
Number of observations with all compared variables equal           5
Number of values unequal                                           0
Table: Variables not shared            
-----------------------
 No variables not shared 
 ------------------------
Tble: Other variables not compared                       
 --------------------------------
 No other variables not compared 
 --------------------------------
Table: Observations not shared                           
 ---------------------------
 No observations not shared 
 ---------------------------
Table: Differences detected by variable
var.x   var.y     n   NAs
------  ------  ---  ----
x1      x1        0     0
x2      x2        0     0
 Table: Differences detected                      
 ------------------------
 No differences detected 
 ------------------------
Table: Non-identical attributes                             
 ----------------------------
 No non-identical attributes 
 ----------------------------

Case3:-

library(diffdf)
diffdf(data1, data2)
No issues were found!

Example 2: Compare Unequal Data Frames

Case1:-

all_equal(data2, data3)
[1] "- Rows in x but not in y: 1, 2, 3, 4, 5\n- Rows in y but not in x: 1, 2, 3, 4, 5\n"

Now its clearly showing as both the data frames are different and the changes.

Case2:-

Now we can try compared function from library arsenal.

library(arsenal)
summary(comparedf(data1, data3))

Compare Object

Table: Summary of data.frames

Table: Summary of data.frames
 version   arg      ncol   nrow
 --------  ------  -----  -----
 x         data1       2      5
 y         data3       2      5
 Table: Summary of overall comparison
 statistic                                                      value
 ------------------------------------------------------------  ------
 Number of by-variables                                             0
 Number of non-by variables in common                               2
 Number of variables compared                                       2
 Number of variables in x but not y                                 0
 Number of variables in y but not x                                 0
 Number of variables compared with some values unequal              1
 Number of variables compared with all values equal                 1
 Number of observations in common                                   5
 Number of observations in x but not y                              0
 Number of observations in y but not x                              0
 Number of observations with some compared variables unequal        5
 Number of observations with all compared variables equal           0
 Number of values unequal                                           5
 Table: Variables not shared
  No variables not shared  
 Table: Other variables not compared 
 No other variables not compared  
 Table: Observations not shared 
 No observations not shared  
 Table: Differences detected by variable
 var.x   var.y     n   NAs
 ------  ------  ---  ----
 x1      x1        5     0
 x2      x2        0     0
 Table: Differences detected
 var.x   var.y    ..row.names..  values.x   values.y    row.x   row.y
 ------  ------  --------------  ---------  ---------  ------  ------
 x1      x1                   1  1          3               1       1
 x1      x1                   2  2          4               2       2
 x1      x1                   3  3          5               3       3
 x1      x1                   4  4          6               4       4
 x1      x1                   5  5          7               5       5
 Table: Non-identical attributes 
 No non-identical attributes 

Case3:-

library(diffdf)
diffdf(data1, data3)

Differences found between the objects!

Remove rows that contain all NA or certain columns in R? »

A summary is given below.

Not all Values Compared Equal
All rows are shown in table below
=============================
Variable No of Differences
x1             5
All rows are shown in table below
========================================
VARIABLE ..ROWNUMBER.. BASE COMPARE
  x1           1         1       3    
  x1           2         2       4    
  x1           3         3       5    
  x1           4         4       6    
  x1           5         5       7   

Example 3: Compare different dimensional Data Frames

Let’s create a another data frame,

Case1:-

data4 <- data.frame(x1 = 3:9,                     
x2 = LETTERS[1:7]) 
all_equal(data2, data4)

[1] “Different number of rows”

Indicates data2 and data 4 contains different number of dimensions.

Case2:-
Now will see how the results appearing in compared

summary(comparedf(data1, data4))
Table: Summary of data.frames
version   arg      ncol   nrow
--------  ------  -----  -----
x         data1       2      5
y         data4       2      7
Table: Summary of overall comparison
statistic                                                      value
------------------------------------------------------------  ------
Number of by-variables                                             0
Number of non-by variables in common                    2
Number of variables compared                                   2
Number of variables in x but not y                                 0
Number of variables in y but not x                                 0
Number of variables compared with some values unequal      1
Number of variables compared with all values equal                 1
Number of observations in common                                5
Number of observations in x but not y                              0
Number of observations in y but not x                              2
Number of observations with some compared variables unequal        5
Number of observations with all compared variables equal           0
Number of values unequal                                           5
Table: Variables not shared
 ------------------------
 No variables not shared
 ------------------------
Table: Other variables not compared
 --------------------------------
 No other variables not compared
 --------------------------------
Table: Observations not shared
version    ..row.names..   observation
--------  --------------  ------------
y                      6             6
y                      7             7
Table: Differences detected by variable
var.x   var.y     n   NAs
------  ------  ---  ----
x1      x1        5     0
x2      x2        0     0
Table: Differences detected
var.x   var.y    ..row.names..  values.x   values.y    row.x   row.y
------  ------  --------------  ---------  ---------  ------  ------
x1      x1                   1  1          3               1       1
x1      x1                   2  2          4               2       2
x1      x1                   3  3          5               3       3
x1      x1                   4  4          6               4       4
x1      x1                   5  5          7               5       5
Table: Non-identical attributes
 ----------------------------
 No non-identical attributes
 ----------------------------

Case3:-

library(diffdf) 
diffdf(data1, data4)

Differences found between the objects! 

A summary is given below. 
There are rows in COMPARE that are not in BASE !!
All rows are shown in table below
   ===============
   ..ROWNUMBER.. 
  ---------------
         6       
         7       
  ---------------
Not all Values Compared Equal
All rows are shown in table below 
  =============================
   Variable  No of Differences 
  -----------------------------
      x1             5         
  -----------------------------
All rows are shown in table below
 ========================================
 VARIABLE  ..ROWNUMBER..  BASE  COMPARE 
  ----------------------------------------
      x1           1         1       3    
      x1           2         2       4    
      x1           3         3       5    
      x1           4         4       6    
      x1           5         5       7    
  ---------------------------------------- 

Conclusion,

However, we tried different packages here and found dplyr package is easy to use and provided quick view of the data sets.
