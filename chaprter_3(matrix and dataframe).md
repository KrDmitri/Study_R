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
head(iris)        # 데이터셋의 앞부분 일부 출력
tail(iris)        # 데이터셋의 뒷부분 일부 출력

str(iris)         # 데이터셋 요약 정보 보기
iris[,5]          # 품종 데이터 보기
unique(iris[,5])  # 품종의 종류 보기(중복 제거-unique)
table(iris[,"Species"])    # 품종의 종류별 행의 개수 세기 🔥
```

## 매트릭스와 데이터프레임에서 사용하는 함수
```R
colSums(iris[,-5])    # 열별 합계
colMeans(iris[,-5])   # 열별 평균
rowSums(iris[,-5])    # 행별 합계
rowMeans(iris[,-5])   # 행별 평균      여기서 iris[,-5]는 5번째 컬럼 빼고 전부를 가리킴

z <- matrix(1:20,nrow=4,ncol=5)
z
t(z)                             # 행과 열 방향 전환

# 조건에 맞는 행과 열의 값 추출 🔥
IR.1 <- subset(iris, Species=="setosa")                  # subset() 함수는 매트릭스에서 작동이 잘 되지 않고, 데이터프레임에 대해 작동이 된다.🔥
IR.1
IR.2 <- subset(iris, Sepal.Length>5.0 & Sepal.Width>4.0)
IR.2
IR.2[,c(2,4)]
```

## 매트릭스와 데이터프레임의 자료구조 확인
```R
class(iris)               # iris 데이터셋의 자료구조 확인
class(state.x77)          # state.x77 데이터셋의 자료구조 확인
is.matrix(iris)           # 데이터셋이 매트릭스인지를 확인하는 함수
is.data.frame(iris)       # 데이터셋이 데이터프레임인지를 확인하는 함수
is.matrix(state.x77)
is.data.frame(state.x77)

# 매트릭스와 데이터프레임의 자료구조 변환
st <- data.frame(state.x77)       # 매트릭스를 데이터프레임으로 변환
head(st)
class(st)

iris.m <- as.matrix(iris[,1:4])   # 데이터프레임을 매트릭스로 변환
head(iris.m)
class(iris.m)
```

## 파일 데이터 읽기/쓰기 (setwd()함수와 read.csv()함수)
```R
setwd("/Users/joseongbeom/Devspace/R/source/Ch03")  # 작업 폴더 지정
air <- read.csv("airquality.csv", header = T)       # .csv 파일 읽기  header=T는 읽어올 파일의 첫 번째 줄을 값이 아닌 열의 이름이라는 뜻
head(air)
```

## 파일 데이터 쓰기 (setwd()함수와 write.csv()함수)
```R
setwd("/Users/joseongbeom/Devspace/R/source/Ch03")  # 작업 폴더 지정
my.iris <- subset(iris, Species == 'setosa')        # setosa 품종 데이터만 추출
write.csv(my.iris, "my_iris.csv", row.names=F)      # .csv 파일에 저장하기  row.names=F는 저장할 때 행 번호를 붙이지 말라는 의미
```

## 함수 정리
cbind() : 벡터, 매트릭스, 데이터프레임 등을 열 방향으로 묶는다.  
rbind() : 벡터, 매트릭스, 데이터프레임 등을 행 방향으로 묶는다.  
rownames() : 행의 이름을 출력한다.  
colnames() : 열의 이름을 출력한다.  
