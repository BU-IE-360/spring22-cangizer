## Welcome to My GitHub Page

### Homework 1
---
title: "HW1"
author: "CAN GİZER"
date: "4/15/2022"
output: html_document
---

```{r setup, include=FALSE}
library(zoo)
library(tidyverse)
library(lubridate)
library(ggplot2)
library(ggcorrplot)
library(openxlsx)
```

# Introduction
  The exchange rates depend on many factors. Interest rates, inflation numbers, political stability are to name a few.This paper will look the relationship between exchange rates, monthly tourism revenues and monthly net imports. 
  Tourism sector is important in Turkish economy. It accounts for roughly 7-8% of GDP and when foreign tourists come, demand for Turkish lira increases, supposedly decreasing the exchange rate.
  Conversely, positive net imports increases the demand for foreign currencies and should increase the exchange rate
```{r DataImport}
setwd("/Users/iremgizer/Desktop")
evds <- read.xlsx("EVDS.xlsx")
```

## Data Import
Instead of downloading the data individually, I have downloaded all the data into a single xlsx file.

```{r , echo=TRUE}
head(evds)
is.data.frame(evds)
colnames(evds) <-  c('Date' , 'Tourism_Revenue_millUSD','Import_thUSD','Export_thUSD', 'Exchange_Rate')
```
To see what's the data I have taken, colnames can be looked. It gives an insight on the data used in this analysis. Using this data, I have accessed to Net Imports in Billions USD,ckeaned the columns  and set the date as date.
```{r , echo=FALSE}
evds$Date <-as.yearmon(evds$Date)
evds$Net_Imports_thUSD <- evds$Import_thUSD-evds$Export_thUSD
evds$Net_Imports_BillUSD <- (evds$Net_Imports_thUSD)/1000000
evds = na.omit(evds)
ggplot(evds, aes(x=Date,Exchange_Rate)) +
  geom_line()
```
As one can see the general trend is upwards for USD/TL exchange rate. One thing to note is, besides summer of 2018, on summer seasons the exchange stays relatively stable and on winter seasons it increases more. On summer of 2018 it increased due to political reasons which will for sure skew the correlation data. 
```{r , echo=FALSE}
ggplot(evds, aes(x=Date,y=Net_Imports_BillUSD)) +
  geom_line()
```
Turkey imports more than it exports. There many reasons for this. Turkey can not produce its own energy mainly because we are not an unrenewable energy rich country. On top of that, Turkey doesn't have mamny natural resources and the overall education level isn't high. All these factors make Turkish manufacturing mainly focus on assembly lines for low to medium tech products. 
```{r , echo=FALSE}
ggplot(evds, aes(Date,Tourism_Revenue_millUSD)) +
  geom_line()
  
```
Turkey imports more than it exports. There many reasons for this. Turkey can not produce its own energy mainly because we are not an unrenewable energy rich country. On top of that, Turkey doesn't have mamny natural resources and the overall education level isn't high. All these factors make Turkish manufacturing mainly focus on assembly lines for low to medium tech products. 
```{r , echo=FALSE}
ggplot(evds, aes(Date,Tourism_Revenue_millUSD)) +
  geom_line()
```
Turkish tourism sector has a strong periodicity. During summer seasons it peaks and during winter it drops significantly. During the start of pandemic, it didn't showed the same periodicity, because of lockdown. One other key takeaway is the tourism revenue peaks during summers are relatively constant. 
```{r , echo=FALSE}
correlations <- cbind(evds$Tourism_Revenue_millUSD,evds$Exchange_Rate,evds$Net_Imports_BillUSD)
corr <- cor(correlations)
colnames(corr)<- c("Tourism","Exchange","Net_Imports")
ggcorrplot(corr, hc.order = TRUE,outline.col = "white",lab=TRUE)
```

Correlation plot shows the exact opposite though. As expected, while the tourism revenue increased, exchange rates have fallen although slightly.As mentioned above, the exchange rates are dependent on many political factors as well. For instance, in the summer of 2018, a political crisis happened between US and Turkey, significantly increasing the exchange rate. Factors outside the nominal values are making it hard to see the underlying correlations between data.
One such situation is between net imports and exchange rate. We would expect that once the net imports are increasing, the exchange rate will increase as well since the demand for foreign currency in Turkey will increase, further increasing its price. However this phenomena can be explained by the other way around. In the early 2010s, when the USD was relatively cheap and Turkey had an import heavy economic policy, importing was rampant and Turkish consumers used foreign goods much more than now. However, with the continous increase in exchange rates the purchasing power of TL severely dropped, making Turkish consumers less likely to purchase foreign goods which are becoming more expensive with each passing day. Chaarts below also depict this relationship.
```{r , echo=FALSE}
ggplot(evds,aes(Net_Imports_BillUSD,Exchange_Rate)) +
  geom_smooth()
```
```{r , echo=FALSE}
ggplot(evds,aes(Tourism_Revenue_millUSD,Exchange_Rate))+ 
  geom_smooth()
```

 # Conclusion 
The relationship between exchange rates, net imports and tourism revenue have been analyzed.
### Homework 2
### Homework 3

[link] (https://moodle.boun.edu.tr/login/)
