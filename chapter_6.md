# 다중변수 자료의 탐색
## 두 변수 사이의 산점도(scatter plot)
산점도란 2개의 변수로 구성된 자료의 분포를 알아보는 그래프로, 관측값들의 분포를 통해 2개의 변수 사이의 관계를 파악할 수 있는 기법이다.  
```R
wt <- mtcars$wt                    # 중량 자료
mpg <- mtcars$mpg                  # 연비 자료
plot(wt,mpg,                       # 2개 변수(x축, y축)
     mian="weight-mileage graph",  # 제목
     xalb="weight",                # x축 레이블
     ylab="mileage(MPG)",          # y축 레이블
     col="red",                    # point의 color
     pch=19)                       # point의 종류
```
<img width="773" alt="스크린샷 2021-09-14 오후 7 39 37" src="https://user-images.githubusercontent.com/86886489/133243336-64d19714-c44d-4b1f-b0ad-362e8b1f3625.png">

## 여러 변수들 간의 산점도
여러 개의 변수에 대해 짝지어진 산점도를 한 번에 그리는 pairs() 함수
```R
vars <- c("mpg","disp","drat","wt")   # 대상 변수
target <- mtcars[,vars]
head(target)
pairs(target,                         # 대상 데이터
      main="Multi Plots")
```
<img width="757" alt="스크린샷 2021-09-14 오후 7 39 00" src="https://user-images.githubusercontent.com/86886489/133243256-4f56fc8a-2db9-418c-9c13-c37c8046d2fd.png">  

## 상관분석(correlation analysis)과 상관계수
선형적 관계에서 강한 선형적 관계가 있고 약한 선형적 관계가 있는데, 얼마나 선형성을 보이는지 수치상으로 나타낼 수 있는 방법이 있어야 하는데, 그 방법이 바로 상관분석이다.  
상관분석은 두 변수 x와 y사이의 선형성 정도를 측정하는 방법으로 다음과 같이 정의된다.  
<img width="383" alt="스크린샷 2021-09-14 오후 7 43 49" src="https://user-images.githubusercontent.com/86886489/133243883-c42252f3-14bb-47ad-b1fb-102fef4a0298.png">
여기서 r을 피어슨 상관계수(Pearson's correlation coefficient), 또는 간단히 줄여서 상관계수(correlation coefficient)라고 부른다. 상관계수는 선형성의 정도를 나타내는 척도로 사용된다.  
상관 계수 r이 1이나 -1에 가까울수록 x,y의 상관성이 높다.  

## R을 이용한 상관계수의 계산
```R
beers = c(5,2,9,8,3,7,3,5,3,5)
bal <- c(0.1,0.03,0.19,0.12,0.04,0.0095,
         0.07,0.06,0.02,0.05)
tbl <- data.frame(beers,bal)
tbl
plot(bal~beers, data=tbl)         # 산점도
res <- lm(bal~beers, data=tbl)    # 회귀식 도출 🔥
abline(res)                       # 회귀선 그리기 🔥
cor(beers,bal)                    # 상관계수 계산 🔥
```
lm() 함수는 두 변수의 선형 관계를 가장 잘 나타낼 수 있는 선의 식(이것을 회귀식이라고 한다.)을 자동으로 찾는 역할을 한다.  
abline() 함수는 회귀식을 이용하여 산점도 위에 선(회귀선)을 그리는 함수이다. 회귀선은 관측값들의 추세를 가장 잘 나타낼 수 있는 선이다.  
cor() 함수는 상관계수를 구하는 역할을 한다. cor()함수는 두 변수 사이의 상관계수를 구하는 역할을 하지만, 여러 개의 변수를 입력하면 여러 개의 변수 사이의 상관계수값을 테이블 형태로 나타낸다.  
<img width="432" alt="스크린샷 2021-09-14 오후 7 55 37" src="https://user-images.githubusercontent.com/86886489/133245366-8a6595e9-e7e3-4c2c-82b8-9effb2fb0611.png">  

# 선그래프
시간의 변화에 따라 자료를 수집한 경우 이를 시계열 자료(times series data)라고 한다.  
## 선그래프의 작성
```R
month = 1:12
late = c(5,8,7,9,4,6,12,13,8,6,6,4)
plot(month,                          # x data
     late,                           # y data
     main="latecomer statistics",
     type = "l",                     # 그래프의 종류 선택(알파벳)
     lty=1,                          # 선의 종류(line type) 선택
     lwd=1,                          # 선의 굵기 선택
     xalb="Month",
     ylab="Late cnt")
```
<img width="1155" alt="스크린샷 2021-09-14 오후 8 00 06" src="https://user-images.githubusercontent.com/86886489/133245950-95cd2d98-4512-4942-baa4-39019ab9429a.png">

## 복수의 선그래프 작성
선그래프는 하나의 선뿐만 아니라 복수의 선도 나타낼 수 있다.  
```R
month = 1:12
late1 = c(5,8,7,9,4,6,12,13,8,6,6,4)
late2 = c(4,6,5,8,7,8,10,11,6,5,7,3)
plot(month,
     late1,
     main="Late Students",
     type="b",
     lty=1,
     col="red",
     xlab="Month",
     ylab="Late cnt",
     ylim=c(1,15)        # y축 값의 (하한, 상한)
)
lines(month,             # lines() 함수는 plot() 함수로 작성한 그래프 위에 선을 겹쳐서 그리는 역할을 한다.
      late2,
      type="b",
      col="blue")
```

# 자료의 탐색 실습(BostonHousing 데이터셋 소개)
```R
## (1) Prepare Data ------------------------
library(mlbench)
data("BostonHousing")
myds <- BostonHousing[,c("crim","rm","dis","tax",
                         "medv")]

## (2) Add new column ------------------------
grp <- c()
for (i in 1:nrow(myds)) {
        if (myds$medv[i] >= 25.0) {
                grp[i] <- "H"
        } else if (myds$medv[i] <= 17.0) {
                grp[i] <- "L"
        } else {
                grp[i] <- "M"
        }
}
grp <- factor(grp)
grp <- factor(grp, levels=c("H","M","L"))

myds <- data.frame(myds, grp)

## (3) Check dataset form ------------------------
str(myds)
head(myds)
table(myds$grp)

## (4) Histogram ------------------------
par(mfrow=c(2,3))
for(i in 1:5) {
        hist(myds[,i],
             main=colnames(myds)[i],
             col="yellow")
}
par(mfrow=c(1,1))

## (5) boxplot ------------------------
par(mfrow=c(2,3))
for(i in 1:5){
        boxplot(
                myds[,i],
                main=colnames(myds)[i]
        )
}
par(mfrow=c(1,1))

## (6) boxplot by group ------------------------
boxplot(myds$crim~myds$grp, main="crime rate per person")
boxplot(myds$rm~myds$grp, main="the number of room")

## (7) scatter plot ------------------------
pairs(myds[,-6])

## (8) scatter plot with group ------------------------
point <- as.integer(myds$grp)
color <- c("red","green","blue")
pairs(myds[,-6],pch=point,col=color[point])

## (9) correlation coefficient ------------------------
cor(myds[,-6])
```
