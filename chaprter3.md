# 매트릭스와 데이터프레임
## 매트릭스
```R
z2 <- matrix(1:20, nrow=4, ncol=5, byrow=T)  # 매트릭스 생성하는 방법
z2
````

## 데이터프레임
```R
city <- c("Seoul","Tokyo","Washington")
rank <- c(1,3,2)
city.info <- data.frame(city,rank)        # 데이터프레임 생성하는 방법
city.info
```

## 데이터셋의 기본 정보 확인
```R
dim(iris)         # 행과 열의 개수 출력
nrow(iris)        # 행의 개수 출력
ncol(iris)        # 열의 개수 출력
colnames(iris)    # 열 이름 출력, names()와 결과 동일
head(iris)        # 데이터셋의 앞부분 일부 출력�
tail(iris)        # 데이터셋의 뒷부분 일부 출력

str(iris)         # 데이터셋 요약 정보 보기
iris[,5]          # 품종 데이터 보기
unique(iris[,5])  # 품종의 종류 보기(중복 제거-unique)
table(iris[,"Species"])    # 품종의 종류별 행의 개수 세기 🐭
```

