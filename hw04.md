Facebook粉絲專頁團分析(分析專頁名稱朱立倫)
================

說明:分析朱立倫總統候選人粉絲專頁，資料分析區間為2016/01/01到2016/04/11。

讀取朱立倫粉絲團資料
--------------------

    if (!require('Rfacebook')){
      install.packages("Rfacebook")
      library(Rfacebook)
    }
    totalPage<-NULL
    lastDate<-Sys.Date()
    numberOfPost<-30
    DateVector<-seq(as.Date("2016-01-01"),lastDate,by="5 days")
    DateVectorStr<-as.character(DateVector)
    token<-'EAACEdEose0cBAI1H3nU5h8JhN6v3dUZBd8xTkAt7ReQZB8o4LpdXQ0q6htg5Uv32Vds3gCxWlpZCSjHm1ezy28Y1ZBvZBoyB0MIV40gpFfnopI3CBK2kOOKngQ6sUZCX7EFB7JV9aYX2rKUmvxIP5FhZAiQPZAFl7hkDWxChYljzlwZDZD'
    for(i in 1:(length(DateVectorStr)-1)){
      tempPage<-getPage("llchu", token,
                        since = DateVectorStr[i],until = DateVectorStr[i+1])
      totalPage<-rbind(totalPage,tempPage)
    }

    ## 14 posts 13 posts 25 posts 4 posts 5 posts 5 posts 7 posts 5 posts 1 posts 6 posts 5 posts 3 posts 4 posts 6 posts 4 posts 8 posts 5 posts 5 posts 4 posts 5 posts 

    nrow(totalPage)

    ##134

討論:2016/01/01至2016/04/11朱立倫粉絲團一共有134篇文章。

每日發文數分析
--------------

說明:分析朱立倫粉絲團每天的發文數，由於日期格式跟台灣不一樣，先將其轉換為台灣時區。

    totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                     format = "%Y-%m-%dT%H:%M:%S+0000", 
                                     tz = "GMT") #2016-01-16T15:05:36+0000
    totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                                tz = "Asia/Taipei") #2016-01-16
    totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
    PostCount<-aggregate(id~dateTPE,totalPage,length)
    library(knitr)
    kable(head(PostCount[order(PostCount$id,decreasing = T),]))

|     | dateTPE    |   id|
|:----|:-----------|----:|
| 12  | 2016-01-12 |    7|
| 13  | 2016-01-13 |    5|
| 14  | 2016-01-14 |    5|
| 15  | 2016-01-15 |    5|
| 65  | 2016-03-20 |    4|
| 1   | 2016-01-01 |    3|

討論:2016/01/12的發文數最多，一共有七篇，2016/01/13和2016/01/14及2016/01/15居次，再來是2016/03/20和2016/01/01，這是因為2016/1/16是總統大選，選前需要拉高知名度，努力得到選民的支持。

每日Likes數分析
---------------

說明:分析朱立倫粉絲團每天的Likes數，由於日期格式跟台灣不一樣，先將其轉換為台灣時區。

    totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                     format = "%Y-%m-%dT%H:%M:%S+0000", 
                                     tz = "GMT") #2016-01-16T15:05:36+0000
    totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                                tz = "Asia/Taipei") #2016-01-16
    totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
    likesCount<-aggregate(likes_count~dateTPE,totalPage,mean)
    library(knitr)
    kable(head(likesCount[order(likesCount$likes_count,decreasing = T),]))

|     | dateTPE    |  likes\_count|
|:----|:-----------|-------------:|
| 16  | 2016-01-16 |       83385.0|
| 34  | 2016-02-06 |       57639.0|
| 9   | 2016-01-09 |       52729.5|
| 15  | 2016-01-15 |       49404.6|
| 17  | 2016-01-18 |       46132.0|
| 36  | 2016-02-08 |       41877.0|

討論:2016/01/16的likes數最多，一共有8萬個讚，2016/02/06居次，再來是2016/01/09，2016/01/16是因為剛剛總統大選完，所以關注度較高，2016/02/06是因為台南地震事件，全台灣民眾都為台灣祈禱的事件，所以關注度高。

每日Comments數分析
------------------

說明:分析朱立倫粉絲團每天的Comments數，由於日期格式跟台灣不一樣，先將其轉換為台灣時區。

    totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                     format = "%Y-%m-%dT%H:%M:%S+0000", 
                                     tz = "GMT") #2016-01-16T15:05:36+0000
    totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                                tz = "Asia/Taipei") #2016-01-16
    totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
    commentsCount<-aggregate(comments_count~dateTPE,totalPage,mean)
    library(knitr)
    kable(head(commentsCount[order(commentsCount$comments_count,decreasing = T),]))

|     | dateTPE    |  comments\_count|
|:----|:-----------|----------------:|
| 16  | 2016-01-16 |          10605.5|
| 15  | 2016-01-15 |           7843.6|
| 17  | 2016-01-18 |           3629.0|
| 9   | 2016-01-09 |           1883.0|
| 18  | 2016-01-19 |           1649.0|
| 34  | 2016-02-06 |           1377.0|

討論:2016/01/16的comments數最多，2016/01/15居次，2016/01/16是總統選舉的日期，故評論高，而2016/01/15為選前一天，評論也會隨之偏高。

每日Shares數分析
----------------

說明:分析朱立倫粉絲團每天的Shares數，由於日期格式跟台灣不一樣，先將其轉換為台灣時區。

    totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                     format = "%Y-%m-%dT%H:%M:%S+0000", 
                                     tz = "GMT") #2016-01-16T15:05:36+0000
    totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                                tz = "Asia/Taipei") #2016-01-16
    totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
    sharesCount<-aggregate(shares_count~dateTPE,totalPage,mean)
    library(knitr)
    kable(head(sharesCount[order(sharesCount$shares_count,decreasing = T),]))

|     | dateTPE    |  shares\_count|
|:----|:-----------|--------------:|
| 15  | 2016-01-15 |       2342.200|
| 1   | 2016-01-01 |       1520.667|
| 16  | 2016-01-16 |       1363.500|
| 34  | 2016-02-06 |       1264.000|
| 12  | 2016-01-12 |       1000.429|
| 9   | 2016-01-09 |        937.000|

討論:2016/01/15分享數最多，2016/01/01和2016/01/16居次，2016/01/15是總統選舉前一天，朱立倫候選人將想表達的理念，在透過支持的民眾分享出去，所以shares數很高，2016/01/01和2016/01/16分別是因為跨年和總統大選後，所以分享度高。
