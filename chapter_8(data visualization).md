# 데이터 시각화(data visualization)
## 데이터 시각화의 중요성
데이터 분석 과정에서 중요한 기술 중의 하나가 바로 데이터 시각화이다. 데이터 시각화는 숫자 형태의 데이터를 그래프나 그림 등의 형태로 표현하는 것이다. 이번 절에서는 실제로 많이 쓰이는 데이터 시각화 기법인 트리맵, 버블차트, 모자이크 플로에 대해 학습하고, 다음 절에서 미적인 그래프를 작성할 수 있도록 지원하는 ggplot에 대해 알아본다.  

## 트리맵(tree map)
트리맵은 사각 타일의 형태로 구성되어 있으며, 각 타일의 크기와 색으로 데이터에 담긴 정보를 표현한다. 또한 각각의 타일은 계층 구조가 있기 때문에 데이터에 존재하는 계층 구조도 표현할 수 있다.

## GNI2014 데이터셋으로 트리맵 작성하기
GNI2014 각 열의 의미  
iso3 : 국가를 식별하는 표준 코드  
country : 국가명  
continent : 국가가 속한 대륙명  
population : 국가의 인구  
GNI : 국가의 국민총소득
```R
library(treemap)                       # treemap 패키지 불러오기
data(GNI2014)                          # 데이터 불러오기
head(GNI2014)                          # 데이터 내용보기
treemap(GNI2014,
        index=c("continent","iso3"),   # 계층구조 설정(대륙-국가)   트리맵 상에서 타일들이 continent 안에 iso3의 형태로 배치되는 것을 지정한다.
        vSize="population",            # 타일의 크기
        vColor="GNI",                  # 타일의 컬러
        type="value",                  # 타일 컬러링 방법
        bg.labels="yellow",            # 레이블의 배경색
        title="World's GNI")           # 트리맵 제목
```
<img width="1074" alt="스크린샷 2021-09-16 오후 9 19 52" src="https://user-images.githubusercontent.com/86886489/133610931-deba603c-8076-42da-91b6-ca1b5aeb43e1.png">  

## state.x77 데이터셋으로 트리맵 작성하기
```R
library(treemap)
st<-data.frame(state.x77)                     # 매트릭스를 데이터프레임으로 변환
st<-data.frame(st, stname=rownames(st))       # 주 이름 열 stname을 추가

treemap(st,
        index=c("stname"),                    # 타일에 주 이름 표기
        vSize="Area",                         # 타일의 크기
        vColor="Income",                      # 타일의 컬러
        type="value",                         # 타일 컬러링 방법
        title="USA states area and income")
```
<img width="1032" alt="스크린샷 2021-09-16 오후 9 20 28" src="https://user-images.githubusercontent.com/86886489/133611026-737681bf-9bae-472e-87dc-e5ac5d86edf3.png">  

## 버블차트(bubble chart)
버블차트는 앞에서 배운 산점도 위에 버블의 크기로 정보를 표시하는 시각화 방법이다. 산점도가 2개의 변수에 의한 위치 정보를 표시한다면, 버블차트는 3개의 변수 정보를 하나의 그래프에 표시한다.  
```R
st<-data.frame(state.x77)              # 매트릭스를 데이터프레임으로 변환
symbols(st$Illiteracy, st$Murder,      # 원의 x,y 좌표의 열
        circles=st$Population,         # 원의 반지름의 열
        inches=0.3,                    # 원의 크기 조절값
        fg="white",                    # 원의 테두리 색
        bg="lightgray",                # 원의 바탕색
        lwd=1.5,                       # 원의 테두리선 두께
        xlab="rate of Illiteracy",
        ylab="crime(murder) rate",
        main="Illiteracy and Crime")
text(st$Illiteracy, st$Murder,         # 텍스트가 출력될 x,y 좌표
     rownames(st),                     # 출력할 텍스트
     cex=0.6,                          # 폰트 크기
     col="brown")                      # 폰트 컬러
```
버블차트는 두 함수 symbols()와 text()의 조합으로 생성된다. symbols()함수는 2차원 좌표 상에 자료값을 원으로 표시하는 기능을 하고 text() 함수는 원 위에 텍스트, 여기서는 주의 이름을 표시하는 기능을 한다.
  <img width="1157" alt="스크린샷 2021-09-16 오후 9 21 00" src="https://user-images.githubusercontent.com/86886489/133611109-4d877444-1474-43fb-a41f-6388fe8c92b1.png">  

## 모자이크 플롯(mosaic plot)
모자이크 플롯은 다중변수 범주형 데이터에 대해 각 변수의 그룹별 비율을 면적으로 표시하여 정보를 전달한다.
```R
head(mtcars)
mosaicplot(~gear+vs, data=mtcars, color=TRUE,
           main="Gear and Vs")
```
위에서 '~gear+vs' 코드는 모자이크 플롯을 작성할 대상 변수를 지정하는데, ~ 다음의 변수가 x축 방향으로 표시되고, + 다음의 변수가 y축 방향으로 표시된다. 
![스크린샷 2021-09-28 오후 8 21 37](https://user-images.githubusercontent.com/86886489/135077525-f7c9e14c-2728-4ddb-8264-ef30a3b33bb7.png)  


## ggplot 패키지
지금까지 우리는 그래프를 작성할 때 주로 R에서 제공하는 기본적인 함수들을 이용하였다. 데이터 분석에 있어서는 기본 함수들만 이용하여도 충분하지만, 보고서용 그래프와 같이 보다 미적인 그래프를 작성하려면 ggplot 패키지를 주로 이용한다. R의 강점 중의 하나가 ggplot이라고 할 만큼 ggplot은 데이터 시각화에서 널리 사용되고 있다.

## ggplot 명령문의 기본 구조
```R
ggplot(data=xx, aes(x=x1,y=x2))+
  geom_xx()+
  geom_yy()+
  ...
```
ggplot은 보통 하나의 ggplot() 함수와 여러 개의 geom_xx() 함수들이 +로 연결되어 하나의 그래프를 완성한다. ggplot() 함수의 매개변수로 그래프를 작성할 때 사용할 데이터셋(data=xx)과 데이터셋 안에서 x축,y축으로 사용할 열 이름(aes(x=x1,y=x2))을 지정한다. 그리고 이 데이터를 이용하여 어떤 형태의 그래프를 그릴지를 geom_xx()를 통해 지정한다. 예를 들면 geom_bar()는 ggplot()함수에서 지정한 데이터를 이용하여 막대그래프를 그리는 경우에 사용한다.  

## 막대그래프의 작성
```R
library(ggplot2)

month <- c(1,2,3,4,5,6)
rain <- c(55,50,45,50,60,70)
df <- data.frame(month, rain)       # 그래프를 작성할 대상 데이터
df

ggplot(df, aes(x=month,y=rain))+    # 그래프를 그릴 데이터 지정
  geom_bar(stat="identity",         # 막대의 높이는 y축에 해당하는 열의 값
           width=0.7,               # 막대의 폭 지정
           fill="steelblue")        # 막대의 색 지정
```
![스크린샷 2021-09-28 오후 8 24 15](https://user-images.githubusercontent.com/86886489/135077867-ac484daa-caf8-47c3-86ad-d18459051021.png)  

## 막대그래프 꾸미기
```R
ggplot(df, aes(x=month,y=rain))+       # 그래프를 그릴 데이터 지정
  geom_bar(stat="identity",            # 막대의 높이는 y축에 해당하는 열의 값
           width=0.7,                  # 막대의 폭 지정
           fill="steelblue")+          # 막대의 색 지정
  ggtitle("monthly precipitation")+    # 그래프의 제목 지정
  theme(plot.title = element_text(size=25, face="bold", colour="steelblue"))+
  labs(x="month", y="precipitation")+  # 그래프의 x, y축 레이블 지정
  coord_flip()                         # 그래프를 가로 방향으로 출력
```
![스크린샷 2021-09-28 오후 8 34 10](https://user-images.githubusercontent.com/86886489/135079160-f9d22e28-341d-41e8-bf87-2d9e9aea5f1a.png)

## 히스토그램의 작성
```R
library(ggplot2)

ggplot(iris, aes(x=Petal.Length))+      # 그래프를 그릴 데이터 지정
  geom_histogram(binwidth=0.5)          # 히스토그램 작성
```
'binwidth=0.5' 의미 : 히스토그램은 연속형 숫자 자료에 대해 일정 길이로 구간을 나눈 후 각 구간에 속하는 자료값이 몇 개 있는지 카운트한다. binwidth는 구간의 길이를 지정하는 매개변수로 이 경우는 꽃잎의 길이를 0.5 간격으로 나누라는 의미이다.  
![스크린샷 2021-09-28 오후 8 52 32](https://user-images.githubusercontent.com/86886489/135081611-20ac29eb-12f5-4d6b-878a-73bfac9b9824.png) 


## 그룹별 히스토그램 작성하기
```R
library(ggplot2)

ggplot(iris, aes(x=Sepal.Width, fill=Species, color=Species))+
  geom_histogram(binwidth=0.5, position="dodge")+
  theme(legend.position="top")
```
'fill=Species' 의미 : 히스토그램의 막대 내부를 채울 색을 지정한다. 여기서는 Species(품종)를 지정했는데, Species(품종)는 팩터 타입이기 때문에 숫자 1, 2, 3으로 변환될 수 있다. 품종별로 막대의 색이 다르게 채워진다.  
'position="dodge"' 의미 : 이 히스토그램은 3개 품종의 히스토그램이 하나의 그래프에 작성된다. 동일 구간에 대해 3개의 막대가 그려진다. position은 동일 구간의 막대들을 어떻게 그릴지를 지정하는데, "dodge"는 막대들을 겹치지 않고 병렬로 그리도록 지정하는 것이다.  

![스크린샷 2021-09-28 오후 9 28 13](https://user-images.githubusercontent.com/86886489/135086565-d50d0b71-3d88-4ba2-840b-9ac8b788ef53.png)  

## 산점도의 작성
```R
library(ggplot2)

ggplot(data=iris, aes(x=Petal.Length, y=Petal.Width)) +
  geom_point()       # 산점도를 작성하는 함수
```

## 그룹이 구분되는 산점도 작성하기
```R
library(ggplot2)

ggplot(data=iris, aes(x=Petal.Length, y=Petal.Width,
                      color=Species)) +
  geom_point(size=3) +
  ggtitle("Petal length and width") +                  # 그래프의 제목 지정
  theme(plot.title=element_text(size=25, face="bold", colour="steelblue"))
```
![스크린샷 2021-09-28 오후 9 37 08](https://user-images.githubusercontent.com/86886489/135088206-8b85856b-5780-47e6-95f1-ec208bd90d90.png)  

## 상자그림의 작성
```R
library(ggplot2)

ggplot(data=iris, aes(y=Petal.Length)) +
  geom_boxplot(fill="yellow")
```

## 그룹별 상자그림 작성하기
```R
ggplot(data=iris, aes(y=Petal.Length, fill=Species)) +
  geom_boxplot()
```

## 선그래프의 작성
```R
library(ggplot2)

year <- 1937:1960
cnt <- as.vector(airmiles)
df <- data.frame(year,cnt)
head(df)

ggplot(data=df, aes(x=year, y=cnt)) +
  geom_line(col="red")
```
![스크린샷 2021-09-28 오후 9 46 45](https://user-images.githubusercontent.com/86886489/135089667-4136b957-ab11-450b-bba4-02a37e24c632.png)  


