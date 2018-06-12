## Study Design
In this analysis, we import data from 2 text files containing data for names in 2015 and 2016. We then merge the data frames and add a
total column that is the sum of name counts from 2015 and 2016. This merged data frame is used for analyzing the most popular names.

## Variables

We have 5 primary data frames used in this analysis.

* y2016 - import of names, gender, and count from yob2016.txt
* y2015 - import of names, gender, and count from yob2015.txt
* final - merge of y2015 and y2016 datasets by FirstName
* sortedFinal - final data frame ordered by Total column
* sortedFinalGirls - sortedFinal data frame with males removed.

## Instructions

1. Create the y2016 data frame

```
df = read.table("yob2016.txt", header = FALSE, col.names = c("FirstName", "Gender", "Count"), sep = ";", colClasses = c("character", "character", "integer"))
misSpelledIndex <-grep("yyy$", df$FirstName)
y2016 <- df[-misSpelledIndex,]
```

2. Create the y2015 data frame

```
y2015 = read.table("yob2015.txt", header = FALSE, col.names = c("FirstName", "Gender", "Count"), sep = ",", colClasses = c("character", "character", "integer"))
```

3. Create the final data frame excluding unmatched rows.

```
final <- merge(y2016, y2015, by = "FirstName", all = FALSE)
colnames(final) <- c("FirstName", "Gender2016", "Count2016", "Gender2015", "Count2015")
final$Total <- with(final, Count2016 + Count2015)
```

4. Create the sortedFinal data frame

```
sortedFinal <- final[order(-final$Total),]
```

5. Create the sortedFinalGirls data frame

```
sortedFinalGirls <- subset(sortedFinal, sortedFinal$Gender2016 == "F" & sortedFinal$Gender2015 == "F")
```
