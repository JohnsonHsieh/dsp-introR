---
title       : 第一次學 R 就上手
subtitle    : 
author      : Johnson Hsieh (謝宗震)
job         : DSP團訓班2
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : zenburn       # 
license     : 
logo        : 
widgets     : [mathjax, bootstrap, quiz]
mode        : selfcontained # {standalone, draft}


---




## Links To Slides
### Link to all slides
http://JohnsonHsieh.github.com/dsp-introR

### Source code on github
http://github.com/JohnsonHsieh/dsp-introR/blob/gh-pages/index.Rmd

--- .segue .dark
## Installing R and Packages

---
## R 簡介
R 是一個程式語言、統計計算與繪圖的整合環境，萌生於貝爾實驗室（Bell Laboratories），主要作者為 John Chambers。其語法與 S 語言（S-Plus）非常相似，提供非常多的統計工具

包含線性與非線性模型（linear and nonlinear modelling）、統計檢定（statistical tests）、時間序列分析（time series analysis）、分類分析（classification）、群集分析（clustering）等相關工具。

---
## R 的優勢
- 免費、開放、佔有率高
- 資源豐富、易於學習
- 非常靈活、適合開發新方法
- 開發時程短、不用考慮計算效率

---
## 下載與安裝
- R 軟體的官方網站為 http://www.r-project.org 
- 在子網站 CRAN (http://cran.r-project.org/) 中下載 R 軟體
- 友善的IDE RStudio http://www.rstudio.com/ide/ (Windows, Mac and Linux)

<img src="http://pluto.huji.ac.il/~msby/StatThink/Screenshots_WinXP/3-R-project-CRAN.PNG", width=40%>
<img src="https://www.rstudio.com/images/screenshots/rstudio-windows_thumb.png", width=40%>

---
## 
<center>
<img src="http://www.ats.ucla.edu/stat/r/seminars/R.svg", width=80%>
</center>

---
## 安裝與載入 R package

```r
# Installing Packages
install.packages('ElemStatLearn', repos='http://cran.csie.ntu.edu.tw/')
install.packages("Hmisc") # Interaction plot
install.packages("rpart") # Recursive partitioning
install.packages("rpart.plot") # Fancy tree plot
install.packages("RColorBrewer") # Nice color palettes

# Loading Packages
library(ElemStatLearn)
library(Hmisc)
library(rpart) 
library(rpart.plot) 
library(RColorBrewer) 
```


--- .segue .dark
## Intro R basic

---
## 基礎教學
- Commands 以空行 (newline) 或分號 (;) 區隔
- R 的指令有大小寫的區分
- 基本數學運算符號 (+, -, *, /, ^)
- 井號 (#) 表示註解，使得該行不執行運算
- 問號 (?) 表示尋求說明檔
- 箭號 (<-) 表示把右邊的結果 assigned 到 R object


```r
# Example here
5 + 5
1 + 2 + 3 * 4 / (5 - 6)
x <- 1
y <- 3
x + y
```


---
## 基礎教學
- 基本資料結構
  * 數值 (1, 0.35, 41.2)
  * 字串 ("男性", "AB")
  * 邏輯 (TRUE, FALSE)
- 基本邏輯運算符號 (>, >=, <, <=, ==, not !=, and &, or |)

```r
a <- 10; b <- "ten"; c <- "25"; d <- TRUE; e <- FALSE 
a > 1 # TRUE
a + b # error
a + c # error
d & e # FALSE
```


---
## 基礎教學
- 確認資料結構 (is.) is.character, is.logical, is.numeric, is.na
- 轉換資料結構 (as.) as.character, as.logical, as.numeric

```r
a <- 10; b <- "ten"; c <- "25"; d <- TRUE; e <- FALSE 
as.numeric(b) # NA
a + as.numeric(c) # 35
as.numeric(d) # 1
as.numeric(e) # 0
as.character(a) #"10"
```


---
## 讀取外部資料
- read.table, read.csv
- 讀進來的R object 稱作 data.frame

```r
# dat <- read.csv("http://johnsonhsieh.github.io/dsp-introR/data/hsb.csv")
dat <- read.csv("data/hsb.csv")
head(dat) # first few rows
```

```
   id    sex  race ses schtyp       prog read write math science socst
1  70   male White   1 public    general   57    52   41      47    57
2 121 female White   2 public vocational   68    59   53      63    61
3  86   male White   3 public    general   44    33   54      58    31
4 141   male White   3 public vocational   63    44   47      53    56
5 172   male White   2 public   academic   47    52   57      53    61
6 113   male White   2 public   academic   44    52   51      63    61
```

```r
class(dat) 
```

```
[1] "data.frame"
```


---
## data.frame 介紹
- 一種類似矩陣 (matrix) 的 R object
- 個別的行或是列，可以存放數值與類別資料
- 利用 object[row,column] 提取資料

```r
dat[1,1]
```

```
[1] 70
```

```r
dat[2, ]
```

```
   id    sex  race ses schtyp       prog read write math science socst
2 121 female White   2 public vocational   68    59   53      63    61
```

```r
dat[, 1]
```

```
  [1]  70 121  86 141 172 113  50  11  84  48  75  60  95 104  38 115  76 195 114  85 167 143  41
 [24]  20  12  53 154 178 196  29 126 103 192 150 199 144 200  80  16 153 176 177 168  40  62 169
 [47]  49 136 189   7  27 128  21 183 132  15  67  22 185   9 181 170 134 108 197 140 171 107  81
 [70]  18 155  97  68 157  56   5 159 123 164  14 127 165 174   3  58 146 102 117 133  94  24 149
 [93]  82   8 129 173  57 100   1 194  88  99  47 120 166  65 101  89  54 180 162   4 131 125  34
[116] 106 130  93 163  37  35  87  73 151  44 152 105  28  91  45 116  33  66  72  77  61 190  42
[139]   2  55  19  90 142  17 122 191  83 182   6  46  43  96 138  10  71 139 110 148 109  39 147
[162]  74 198 161 112  69 156 111 186  98 119  13  51  26  36 135  59  78  64  63  79 193  92 160
[185]  32  23 158  25 188  52 124 175 184  30 179  31 145 187 118 137
```


---
## data.frame 介紹
- 可以用向量 (c) 來提取資料
- 也可以用 object[, "variable"] 或是 object$variable 提取

```r
dat[c(1, 2, 3, 4), "id"]
```

```
[1]  70 121  86 141
```

```r
dat$id[1:4]
```

```
[1]  70 121  86 141
```

```r
dat[1:2, c("id", "sex", "write")]
```

```
   id    sex write
1  70   male    52
2 121 female    59
```


---
## data.frame 介紹

```r
dim(dat) # [1] 200 11
```


```r
str(dat) # show dataset structure
```

```
'data.frame':	200 obs. of  11 variables:
 $ id     : int  70 121 86 141 172 113 50 11 84 48 ...
 $ sex    : Factor w/ 2 levels "female","male": 2 1 2 2 2 2 2 2 2 2 ...
 $ race   : Factor w/ 4 levels "African American",..: 4 4 4 4 4 4 1 3 4 1 ...
 $ ses    : int  1 2 3 3 2 2 2 2 2 2 ...
 $ schtyp : Factor w/ 2 levels "private","public": 2 2 2 2 2 2 2 2 2 2 ...
 $ prog   : Factor w/ 3 levels "academic","general",..: 2 3 2 3 1 1 2 1 2 1 ...
 $ read   : int  57 68 44 63 47 44 50 34 63 57 ...
 $ write  : int  52 59 33 44 52 52 59 46 57 55 ...
 $ math   : int  41 53 54 47 57 51 42 45 54 52 ...
 $ science: int  47 63 58 53 53 63 53 39 58 50 ...
 $ socst  : int  57 61 31 56 61 61 61 36 51 51 ...
```


---
## Basic description

```r
summary(dat) # show basic description
```

```
       id            sex                    race          ses           schtyp            prog    
 Min.   :  1.0   female:109   African American: 20   Min.   :1.00   private: 32   academic  :105  
 1st Qu.: 50.8   male  : 91   Asian           : 11   1st Qu.:2.00   public :168   general   : 45  
 Median :100.5                Hispanic        : 24   Median :2.00                 vocational: 50  
 Mean   :100.5                White           :145   Mean   :2.06                                 
 3rd Qu.:150.2                                       3rd Qu.:3.00                                 
 Max.   :200.0                                       Max.   :3.00                                 
      read          write           math         science         socst     
 Min.   :28.0   Min.   :31.0   Min.   :33.0   Min.   :26.0   Min.   :26.0  
 1st Qu.:44.0   1st Qu.:45.8   1st Qu.:45.0   1st Qu.:44.0   1st Qu.:46.0  
 Median :50.0   Median :54.0   Median :52.0   Median :53.0   Median :52.0  
 Mean   :52.2   Mean   :52.8   Mean   :52.6   Mean   :51.9   Mean   :52.4  
 3rd Qu.:60.0   3rd Qu.:60.0   3rd Qu.:59.0   3rd Qu.:58.0   3rd Qu.:61.0  
 Max.   :76.0   Max.   :67.0   Max.   :75.0   Max.   :74.0   Max.   :71.0  
```


---
## Basic description

```r
c(mean(dat$read), sd(dat$read)) # mean and standard deviation
```

```
[1] 52.2 10.3
```

```r
score <- dat[, c("read", "write", "math", "science", "socst")]
cor(score) # correlation
```

```
         read write  math science socst
read    1.000 0.597 0.662   0.630 0.621
write   0.597 1.000 0.617   0.570 0.605
math    0.662 0.617 1.000   0.631 0.544
science 0.630 0.570 0.631   1.000 0.465
socst   0.621 0.605 0.544   0.465 1.000
```


--- .segue .dark
## Modifying and Managing Data

---
## Labeling Categorical Vars

```r
race <- factor(dat$race, 
               levels = c("Hispanic", "Asian", "African American", "White"), 
               labels = c("HI", "AS", "AA", "WH"))
head(race, n=10)
```

```
 [1] WH WH WH WH WH WH AA HI WH AA
Levels: HI AS AA WH
```



--- 
## Sorting Data

```r
dat <- dat[order(dat$id, dat$sex), ] # sort data by id and sex
head(dat)
```

```
    id    sex     race ses schtyp       prog read write math science socst
99   1 female Hispanic   1 public vocational   34    44   40      39    41
139  2 female Hispanic   2 public vocational   39    41   33      42    41
84   3   male Hispanic   1 public   academic   63    65   48      63    56
112  4 female Hispanic   1 public   academic   44    50   41      39    51
76   5   male Hispanic   1 public   academic   47    40   43      45    31
149  6 female Hispanic   1 public   academic   47    41   46      40    41
```


---
## Recoding Data

```r
dat$total <- rowSums(dat[,7:10]) # read + write + math + science
dat$grade <- cut(dat$total,
  breaks = c(0, 140, 180, 210, 234, 300),
  labels = c("F", "D", "C", "B", "A"))
summary(dat[, c("total", "grade")])
```

```
     total     grade 
 Min.   :139   F: 1  
 1st Qu.:180   D:51  
 Median :210   C:50  
 Mean   :210   B:49  
 3rd Qu.:234   A:49  
 Max.   :277         
```


---
## Merging Data
- Use rbind or cbind

```r
dat.female <- dat[dat$sex=="female",]
dat.male <- dat[dat$sex=="male",]
dat.both <- rbind(dat.female, dat.male)
cbind(dim(dat.female), dim(dat.male),dim(dat.both))
```

```
     [,1] [,2] [,3]
[1,]  109   91  200
[2,]   13   13   13
```


--- .segue .dark
## Analyzing Real Data

---
## 台北市實價登錄資料

```r
# Windows
# f <- file("http://johnsonhsieh.github.io/dsp-introR/data/dsp-gift-2013-big5/%E8%B2%B7%E8%B3%A3st_A_10109_10109.csv", encoding="big5")
# f <- file("data/dsp-gift-2013-big5/買賣st_A_10109_10109.csv", encoding="big5")
# Mac, Linux
f <- file("data/dsp-gift-2013-utf8/買賣st_A_10109_10109.csv", encoding="UTF-8-BOM")
tab <- read.csv(f, header=TRUE)
View(tab)
names(tab)
```

```
 [1] "鄉鎮市區"                  "交易標的"                  "土地區段位置.建物區段門牌"
 [4] "土地移轉總面積.平方公尺."  "使用分區或編定"            "非都市土地使用分區"       
 [7] "非都市土地使用地"          "交易年月"                  "交易筆棟數"               
[10] "移轉層次"                  "總樓層數"                  "建物型態"                 
[13] "主要用途"                  "主要建材"                  "建築完成年月"             
[16] "建物移轉總面積.平方公尺."  "建物現況格局.房"           "建物現況格局.廳"          
[19] "建物現況格局.衛"           "建物現況格局.隔間"         "有無管理組織"             
[22] "總價.元."                  "單價.元.平方公尺."         "車位類別"                 
[25] "車位移轉總面積.平方公尺."  "車位總價.元."              "交易標的橫坐標"           
[28] "交易標的縱坐標"           
```



---
## Modifying and Managing Data

```r
tab1 <- tab[, c("鄉鎮市區", "交易標的", "建物型態", "總價.元.", "建物移轉總面積.平方公尺.",
                   "車位總價.元.", "車位移轉總面積.平方公尺.")]
names(tab1) <- c("行政區", "交易標的", "建物型態", "總價", "總面積", "車位價", "車位面積")
# levels(tab1$交易標的); levels(tab1$建物型態)
tab1$交易標的 <- factor(tab1$交易標的, levels(tab1$交易標的), 
                           labels=c("車位","房地","房地+車位","建物","土地"))
tab1$建物型態 <- factor(tab1$建物型態, levels(tab1$建物型態), 
                           labels=c("商辦","廠辦","店面","公寓","華廈","其他",
                                    "套房","透天","大樓"))
head(tab1)
```

```
  行政區  交易標的 建物型態     總價 總面積  車位價 車位面積
1 中正區      房地     華廈 12800000  111.2       0      0.0
2 萬華區      房地     公寓  8500000   79.1       0      0.0
3 大同區      車位     其他  2500000   41.2 2500000     41.2
4 內湖區      房地     商辦  7180000   43.8       0      0.0
5 中山區      房地     大樓 13500000   76.1       0      0.0
6 內湖區 房地+車位     大樓 15500000  100.8       0     16.5
```


---
## Modifying and Managing Data

```r
tab1$房價.萬元 <- (tab1$總價 - tab1$車位價)/10^4
tab1$建物面積.坪 <- 0.3025*(tab1$總面積 - tab1$車位面積)
tab2 <- tab1[tab1$交易標的!="車位",]
tab2 <- tab2[, c("行政區","建物型態","房價.萬元","建物面積.坪")]
head(tab2)
```

```
  行政區 建物型態 房價.萬元 建物面積.坪
1 中正區     華廈      1280        33.6
2 萬華區     公寓       850        23.9
4 內湖區     商辦       718        13.2
5 中山區     大樓      1350        23.0
6 內湖區     大樓      1550        25.5
7 內湖區     公寓      1393        35.3
```


---
## Exploratory Data Analysis

```r
summary(tab2)
```

```
     行政區       建物型態     房價.萬元       建物面積.坪  
 中山區 :259   大樓   :617   Min.   :     0   Min.   :   0  
 北投區 :257   公寓   :364   1st Qu.:   840   1st Qu.:  15  
 內湖區 :233   華廈   :320   Median :  1469   Median :  28  
 文山區 :150   其他   :198   Mean   :  3011   Mean   :  41  
 大安區 :143   套房   :125   3rd Qu.:  2560   3rd Qu.:  45  
 中正區 :128   商辦   : 39   Max.   :670000   Max.   :4430  
 (Other):564   (Other): 71                                  
```


---
## Exploratory Data Analysis

```r
table(tab2[,1])
```

```

北投區 大安區 大同區 南港區 內湖區 士林區 松山區 萬華區 文山區 信義區 中山區 中正區 
   257    143     61     83    233    111     92    108    150    109    259    128 
```

```r
table(tab2[,2])
```

```

商辦 廠辦 店面 公寓 華廈 其他 套房 透天 大樓 
  39   15   31  364  320  198  125   25  617 
```


---
## Pivot tables

```r
# install.packages("reshape", repos="http://cran.rstudio.com")
library(reshape)
cast(tab2, 建物型態 ~ ., fun.aggregate=mean, value="房價.萬元")
```

```
  建物型態 (all)
1     商辦 40033
2     廠辦  5393
3     店面  4751
4     公寓  1417
5     華廈  1917
6     其他  1909
7     套房   789
8     透天  4849
9     大樓  2763
```

---
## Pivot tables

```r
cast(tab2, 行政區 ~ ., fun.aggregate=table, value="建物型態")
```

```
   行政區 商辦 廠辦 店面 公寓 華廈 其他 套房 透天 大樓
1  北投區    0    0    0   37   33   47   11    6  123
2  大安區    3    0    2   23   45   19    9    0   42
3  大同區    1    0    4    9    7   10    7    2   21
4  南港區    3    0    2   22   23    7    2    0   24
5  內湖區   11   15    2   61   48   10    5    5   76
6  士林區    1    0    3   29   24   31    4    5   14
7  松山區    3    0    1   23   19    7    6    0   33
8  萬華區    1    0    2   18   15    9    7    4   52
9  文山區    0    0    1   49   31    9   11    1   48
10 信義區    1    0    4   40    8   23    5    0   28
11 中山區   11    0    8   37   52   11   49    1   90
12 中正區    4    0    2   16   15   15    9    1   66
```


---
## 小挑戰
- 請計算台北市各行政區為的平均房價
- 請計算台北市各行政區各種建物型態的房價中位數
- Hint: use cast function in reshape package, 中位數函數 median

---
## Pie Chart and Bar Chart

```r
par(family="STHeiti") # Mac 中文字型設定
par(mfrow=c(1,2)) # 以兩欄顯示圖形
pie(sort(table(tab2$行政區), decreasing=TRUE))
barplot(sort(table(tab2$建物型態), decreasing=TRUE), las=2)
```

<div class="rimage center"><img src="figure/unnamed-chunk-23.png" title="plot of chunk unnamed-chunk-23" alt="plot of chunk unnamed-chunk-23" class="plot" /></div>


---
## Histogram and denstiy

```r
par(family="STHeiti", mfrow=c(1,2)) # Mac 中文字型設定
id <- tab2$建物型態 == "大樓" | tab2$建物型態 == "華廈" | tab2$建物型態 == "公寓"
tab3 <- tab2[id, ] # 一般住宅建物
tab3 <- tab3[tab3$房價.萬元>500, ]
hist(tab3$建物面積.坪)
hist(tab3$建物面積.坪, breaks=10, col="lightblue", prob=TRUE)
lines(density(tab3$建物面積.坪, bw=8), col=2, lwd=2)
```

<div class="rimage center"><img src="figure/unnamed-chunk-24.png" title="plot of chunk unnamed-chunk-24" alt="plot of chunk unnamed-chunk-24" class="plot" /></div>


---
## 小挑戰
- 改變 hist() 函數中的breaks參數，觀察直方圖的變化
- 改變 density() 函數中的bw參數，觀察機率密度函數的變化


---

```r
par(family="STHeiti", mfrow=c(2,2)) # Mac 中文字型設定
hist(tab3$房價.萬元)
hist(tab3$建物面積.坪)
hist(log10(tab3$房價.萬元))
hist(log10(tab3$建物面積.坪))
```

<div class="rimage center"><img src="figure/unnamed-chunk-25.png" title="plot of chunk unnamed-chunk-25" alt="plot of chunk unnamed-chunk-25" class="plot" /></div>


---

```r
par(family="STHeiti", mfrow=c(1,2)) # Mac 中文字型設定
plot(tab3$房價.萬元, tab3$建物面積.坪, xlab="房價(萬元)", ylab="面積(坪)")
plot(tab3$房價.萬元, tab3$建物面積.坪, xlab="log房價(萬元)", ylab="log面積(坪)", log="xy")
```

<div class="rimage center"><img src="figure/unnamed-chunk-26.png" title="plot of chunk unnamed-chunk-26" alt="plot of chunk unnamed-chunk-26" class="plot" /></div>


---
## Regression

```r
x <- tab3$房價.萬元
y <- tab3$建物面積.坪
cor(x, y)
```

```
[1] 0.809
```

```r
cor(log10(x), log10(y))
```

```
[1] 0.848
```


---

```r
fit <- lm(log10(y) ~ log10(x))
summary(fit) # log10.y = -0.81 + 0.72*log10.x or y = 0.15 * x^0.72
```

```

Call:
lm(formula = log10(y) ~ log10(x))

Residuals:
    Min      1Q  Median      3Q     Max 
-0.4807 -0.0769  0.0036  0.0901  0.5546 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -0.8110     0.0417   -19.5   <2e-16 ***
log10(x)      0.7187     0.0128    56.3   <2e-16 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 0.127 on 1241 degrees of freedom
Multiple R-squared:  0.719,	Adjusted R-squared:  0.718 
F-statistic: 3.17e+03 on 1 and 1241 DF,  p-value: <2e-16
```


---

```r
par(family="STHeiti") # Mac 中文字型設定
plot(x, y, , xlab="房價(萬元)", ylab="面積(坪)", log="xy")
abline(fit, col=2, lwd=2)
text(6000, 20, "log10.y = -0.81 + 0.72*log10.x", col=2, cex=1.5)
```

<div class="rimage center"><img src="figure/unnamed-chunk-29.png" title="plot of chunk unnamed-chunk-29" alt="plot of chunk unnamed-chunk-29" class="plot" /></div>


---
## Prediction

```r
new <- data.frame(x = c(500, 800, 1600, 2500, 5000, 8000))
10^predict(fit, newdata=new)
```

```
   1    2    3    4    5    6 
13.5 18.9 31.0 42.8 70.4 98.7 
```


---
## References
- [Introducing R](http://www.ats.ucla.edu/stat/r/seminars/intro.htm), UCLA R seminars
- [Introduction to R](https://www.datacamp.com/courses/introduction-to-r), DataCamp
- [R的資料型態](http://rpubs.com/wush978/R_DataType), TW R User Group
- [R 簡介](http://statlab.nchc.org.tw/rnotes/?page_id=2), R 學習筆記
- [免費電子書 -- R 統計軟體](http://ccckmit.wikidot.com/r:main), 陳鍾誠的網站
- [StackOverflow](http://stackoverflow.com/), getting help online
