# 단일변수 자료의 탐색
## 자료의 특성에 따른 분류
1. 범주형 자료(categorical data) : 질적 자료(qualitative data)  
2. 연속형 자료(numerical data) : 양적 자료(quantitative data)  
  
범주형 자료는 질적 자료라고도 부르며, 성별과 같이 범주 또는 그룹으로 구분할 수 있는 값으로 구성된 자료를 말한다. 범주형 자료의 값들은 기본적으로 숫자로는 표형할 수 없고, 대소 비교나 산술연산이 적용되지 않는다.  
범주형 자료에 대해서 할 수 있는 기본적인 작업은 자료에 포함된 관측값들의 종류별로 개수를 세는 것이다. 그러면 종류별로 비율을 알 수 있고, 이 결과를 이용하여 막대그래프나 원그래프를 작성할 수 있다.  
예시) 성별, 혈액형, 선호하는 색, 찬성 여부  
  
연속형자료는 양적 자료라고도 부르며, 크기가 있는 숫자들로 구성된 자료를 말한다.  
예시) 몸무게, 키, 일평균 온도, 자녀의 수

## 변수의 개수에 따른 분류
1. 단일변수 자료(univariate data) : 일변량 자료  예시) 변수가 '몸무게' 단 하나  
2. 다중변수 자료(multivariate data) : 다변량 자료  예시) 변수가 '키, 몸무게, 성별' 여러개  
단일변수 자료는 벡터에, 다중변수 자료는 매트릭스 또는 데이터프레임에 저장하여 분석을 진행한다.  

# 단일변수 범주형 자료의 탐색
## 도수분포표의 작성
```R
favorite <- c('winter', 'summer', 'spring', 'summer', 'summer', 'fall',
              'fall', 'summer','spring','spring')
favorite                           # favorite의 내용 출력
table(favorite)                    # 도수분포표 계산
table(favorite)/length(favorite)   # 비율 출력
```

## 막대그래프의 작성
```R
favorite <- c('winter', 'summer', 'spring', 'summer', 'summer', 'fall',
              'fall', 'summer','spring','spring')
favorite

ds <- table(favorite)
ds
barplot(ds, main='favorite season')
```
![스크린샷 2021-09-12 오후 7 52 52](https://user-images.githubusercontent.com/86886489/132984789-00746279-b0c8-4e10-991b-cb89a3a0b740.png)  
barplot()함수는 다양한 매개변수를 가질 수 있으며, 매개변수값에 따라 막대의 색을 다르게 하거나 x축, y축의 레이블을 지정할 수도 있다.  

## 도수분포표 데이터의 순서 정렬
![스크린샷 2021-09-12 오후 7 42 46](https://user-images.githubusercontent.com/86886489/132984504-e57a939e-17a9-47aa-9f71-785e2f14cad4.png)

## 원그래프의 작성
```R
favorite <- c('winter', 'summer', 'spring', 'summer', 'summer', 'fall',
              'fall', 'summer','spring','spring')
favorite

ds <- table(favorite)

ds
pie(ds, main='favorite season')
```
![스크린샷 2021-09-12 오후 7 52 26](https://user-images.githubusercontent.com/86886489/132984779-6624696d-cbfd-410f-9253-9a06719d8e07.png)

## 숫자로 표현된 범주형 자료
```R
favorite.color <- c(2,3,2,1,1,2,2,1,3,2,1,3,2,1,2)
ds <- table(favorite.color)
ds
barplot(ds, main='favorite color')
colors<-c('green', 'red', 'blue')
names(ds) <- colors                 # 자료값 1,2,3을 green, red, blue로 변경
ds
barplot(ds, main='favorite color', col=colors)   # 색 지정 막대그래프
pie(ds, main='favorite color', col=colors)       # 색 지정 원그래프
```

# 단일변수 연속형 자료의 탐색
연속형 자료는 관측값들이 크기를 가지기 때문에 범주형 자료에 비해 다양한 분석 방법이 존재한다.  
## 평균과 중앙값
절사평균(trimmed mean) : 평균이 자료 내에 있는 너무 작거나 큰 관측값의 영향을 받는 것을 완화시키기 위해 제안된 방식으로, 절사평균은 자료의 관측값들 중에서 작은 값들의 하위 n%와 큰 값들의 상위 n%를 제외하고 중간에 있는 나머지 값들만 가지고 평균을 계산한다.  
```R
weight <- c(60,62,64,65,68,69)
weight.heavy <- c(weight, 120)
weight
weight.heavy

mean(weight)                  # 평균
mean(weight.heavy)

median(weight)                # 중앙값
median(weight.heavy)

mean(weight, trim=0.2)        # 절사평균(상하위 20% 제외)
mean(weight.heavy, trim=0.2)
```

## 사분위수(quatrile)
사분위수는 주어진 자료에 있는 값들을 크기순으로 나열했을 때 이것을 4등분하는 지점에 있는 값들을 의미한다. 자료에 있는 값들을 4등분하면 등분점이 3개 생기는데, 앞에서부터 '1사분위수(Q1)','2사분위수(Q2)','3사분위수(Q3)','4사분위수(Q4)'라고 부르며, 2사분위수는 중앙값과 동일하다.  
```R
mydata <- c(60,62,64,65,68,69,120)
quantile(mydata)
quantile(mydata, (0:10)/10)     # 10% 단위로 구간을 나누어 계산
summary(mydata)
```
실행 결과
![스크린샷 2021-09-12 오후 10 27 17](https://user-images.githubusercontent.com/86886489/132989418-f76851ef-f606-4e17-ab1c-adae54418d76.png)  

## 산포(distribution)
산포란 주어진 자료에 있는 값들이 퍼져 있는 정도를 말하며, 자료를 파악할 수 있는 특징 중의 하나이다.  
어떤 자료의 분산(variance)과 표준편차(standard deviation)가 작다는 의미는 자료의 관측값들이 평균값 부근에 모여 있다는 뜻이다.  
```R
mydata <- c(60,62,64,65,68,69,120)
var(mydata)               # 분산
sd(mydata)                # 표준편차
range(mydata)             # 값의 범위
diff(range(mydata))       # 최댓값, 최솟값의 차이
```

## 히스토그램
hist() 함수 이용
```R
dist <- cars[,2]                       # 자동차 제동거리
hist(dist,                             # 자료(data)
     main="Histogram for distance",    # 제목
     xlab="distance",                  # x축 레이블
     ylab="frequency",                 # y축 레이블
     border="blue",                    # 막대 테두리색
     col="green",                      # 막대 색
     las=2,                            # x축 글씨 방향(0~3)
     breaks=5)                         # 막대 개수 조절
```

## 막대그래프와 히스토그램 비교
히스토그램은 외관상 막대그래프와 유사하다. 일반적으로 막대 사이에 간격이 있으면 막대그래프, 간격 없이 막대들이 붙어 있으면 히스토그램이라고 생각하여 구분할 수 있다. 또한 막대그래프에서는 막대의 면적이 의미가 없지만 히스토그램에서는 막대의 면적도 의미가 있다.  

## 상자그림(box plot)
상자그림은 상자 수염 그림(box and whisker plot)으로도 부르며, 사분위수를 시각화하여 그래프 형태로 나타낸 것이다.  
![스크린샷 2021-09-12 오후 10 42 37](https://user-images.githubusercontent.com/86886489/132989923-c5c47118-9c53-4b09-8eb6-a96ded59abb2.png)  
```R
dist <- cars[,2]
boxplot(dist, main="car breaking distance")

# boxplot.stats() 함수를 사용하여 자료의 최솟값, 최댓값, 중앙값 등의 정확한 값 알아보기
boxplot.stats(dist)
```
![스크린샷 2021-09-12 오후 10 47 33](https://user-images.githubusercontent.com/86886489/132990117-8223a547-bbaf-48be-93ce-be211bbee90f.png)  
$stats에는 정상범위 자료의 4분위수에 해당하는 값들이 표시된다. 5개의 값은 차례로 최솟값, 1사분위수, 중앙값, 3사분위수, 최댓값을 의미한다.  
$n의 값은 자료에 있는 관측값들의 개수로, 총 50개의 관측값을 저장하고 있다는 것을 의미한다.  
$conf는 중앙값에 관련된 신뢰 구간을 의미한다.  
$out은 특이값의 목록을 알려주는데, 만일 특이값들만 출력하려면 boxplot.stats(dist)$out과 같은 명령문을 사용한다.  

## 그룹이 있는 자료의 상자그림
```R
boxplot(Petal.Length~Species, data=iris, main="length of petals by species")    #품종별 꽃잎의 길이
```

## 한 화면에 그래프 여러 개 출력하기
```R
par(mfrow=c(1,3))                       # 1*3 가상화면 분할(1행 3열의 화면으로 분할하라는 코드)
barplot(table(mtcars$carb),
        main="Barplot of Carburetors",
        xlab="#of carburetors",
        ylab="frequency",
        col="blue")
barplot(table(mtcars$cyl),
        main="Barplot of Cylender",
        xlab="#of cylender",
        ylab="frequency",
        col="red")
barplot(table(mtcars$gear),
        main="Barplot of Gear",
        xlab="#of gears",
        ylab="frequency",
        col="green")
par(mfrow=c(1,1))                       # 가상화면 분할 해제
```
![스크린샷 2021-09-12 오후 11 04 52](https://user-images.githubusercontent.com/86886489/132990690-ad6a285b-82a0-451f-afd2-c3a295e76475.png)  

## 팁
단일변수 범주형 자료는 도수분포표(table()), 막대그래프(barplot()), 원그래프(pie())를 활용하여 시각화를 한다.
