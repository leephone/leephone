#NBA2014-2015球季各隊分析
#install.packages("SportsAnalytics")
#install.packages("knitr")
library(SportsAnalytics)
NBA1415<-fetch_NBAPlayerStatistics("14-15")

##各隊最辛苦的球員

MaxTotalMinutesPlayed<-aggregate(TotalMinutesPlayed~Team,NBA1415,max)
NBA1415MaxTotalMinutesPlayed<-merge(NBA1415,MaxTotalMinutesPlayed)
output<-NBA1415MaxTotalMinutesPlayed[order(NBA1415MaxTotalMinutesPlayed$TotalMinutesPlayed,decreasing = T),c("Team","Name","TotalMinutesPlayed")]
library(knitr)
kable(output, digits=2)

##各隊得分王

MaxPoint<-aggregate(TotalPoints~Team,NBA1415,max)
NBA1415MaxPoint<-merge(NBA1415,MaxPoint)
output<-NBA1415MaxPoint[order(NBA1415MaxPoint$TotalPoints,decreasing = T),c("Team","Name","TotalPoints")]
library(knitr)
kable(output, digits=2)

##各隊最有效率的球員

maxe<-aggregate(TotalPoints/TotalMinutesPlayed~Name,NBA1415,max)
NBA1415Maxe<-merge(NBA1415,maxe)
output<-NBA1415Maxe[order(NBA1415Maxe$'TotalPoints/TotalMinutesPlayed',decreasing = T),c("Team","Name","TotalPoints/TotalMinutesPlayed")]
library(knitr)
kable(output, digits=2)

##各隊三分球出手最準的球員

maxe<-aggregate(ThreesMade/ThreesAttempted~Name,NBA1415,max)
NBA1415Maxe<-merge(NBA1415,maxe)
output<-NBA1415Maxe[order(NBA1415Maxe$'ThreesMade/ThreesAttempted',decreasing = T),c("Team","Name","ThreesMade/ThreesAttempted")]
library(knitr)
kable(output, digits=2)