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
