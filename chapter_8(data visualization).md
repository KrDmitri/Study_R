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
