# 데이터 전처리
데이터 분석을 제대로 하기 위해서는 초기에 확보한 데이터를 정제하고 가공해서 분석에 적합한 데이터를 확보해야 한다. 이러한 과정을 데이터 전처리(data preprocessing)라고 한다.  
## 결측값의 개념
결측값(missing value)은 데이터를 수집하고 저장하는 과정에서 저장할 값을 얻지 못하는 경우 발생한다. 이러한 결측값을 처리하는 방법은 다음의 두 가지 방법이 있다.  
* 결측값을 제거하거나 제외한 다음 데이터를 분석한다.
* 결측값을 추정하여 적당한 값으로 치환한 후 데이터를 분석한다.

## 결측값의 특성과 존재 여부 확인
```R
z <- c(1,2,3,NA,5,NA,8)
sum(z)                   # 정상 계산이 안 됨
is.na(z)                 # NA 여부 확인
sum(is.na(z))            # NA의 개수 확인
sum(z, na.rm=TRUE)       # NA를 제외하고 합계를 계산
```

## 결측값 대체 및 제거
```R
z1 <- c(1,2,3,NA,5,NA,8)
z2 <- c(5,8,1,NA,3,NA,7)
z1[is.na(z1)] <- 0            # NA를 0으로 치환
z1
z3 <- as.vector(na.omit(z2))  # NA를 제거하고 새로운 벡터 생성
z3
```

## 결측값이 포함된 데이터프레임 생성
```R
x <- iris
x[1,2] <- NA; x[1,3] <- NA
x[2,3] <- NA; x[3,4] <- NA
head(x)
```

## 데이터프레임의 열별 결측값 확인
```R
# for문을 이용한 방법
for (i in 1:ncol(x)) {
        this.na <- is.na(x[,i])
        cat(colnames(x)[i], "\t", sum(this.na), "\n")
}

# apply를 이용한 방법
col_na <- function(y) {
        return(sum(is.na(y)))
}

na_count <- apply(x, 2, FUN=col_na)
na_count
```

## 데이터프레임의 행별 결측값 확인
```R
rowSums(is.na(x))          # 행별 NA의 개수
sum(rowSums(is.na(x))>0)   # NA가 포함된 행의 개수

sum(is.na(x))              # 데이터셋 전체에서 NA 개수
```

## 결측값을 제외하고 새로운 데이터셋 만들기
complete.cases() 함수 사용
```R
head(x)
x[!complete.cases(x),]        # NA가 포함된 행들 출력
y <- x[complete.cases(x),]    # NA가 포함된 행들 제거
head(y)                       # 새로운 데이터셋 y의 내용 확인
```

## 🔥 NA 값이 많은 데이터 처리
어떤 데이터셋은 NA 값을 포함한 행이 많아 이를 모두 제거하면 남는 것이 별로 없어서 데이터를 분석하기 어려운 경우가 있다. 이런 경우에 만약 NA 값이 특정 열에 몰려 있다면 그 열은 제외하고 데이터를 분석한다. NA값이 여러 열에 흩어져 있는 경우는 NA 값을 적당한 값으로 추정하여 대체한 후 분석할 수 있다.

## 특이값의 개념(outlier)
특이값은 정상적이라고 생각되는 데이터의 분포 범위 밖에 위치하는 값들을 말하며, '이상치'라고도 부른다. 데이터 분석에서는 특이값을 포함한 채 평균 등을 계산하면 전체 데이터의 양상을 파악하는데 왜곡을 가져올 수 있으므로 분석할 때 특이값을 제외하는 경우가 많다.  
데이터셋에 특이값이 포함되어 있는지 여부는 다음과 같은 기준을 가지고 찾도록 한다.  
1. 논리적으로 있을 수 없는 값이 있는지 찾아본다.
2. 상식을 벗어난 값이 있는지 찾아본다.
3. 상자그림(boxplot)을 통해 찾아본다.

## 상자그림을 통한 특이값 확인
```R
st <- data.frame(state.x77)
boxplot(st$Income)
boxplot.stats(st$Income)$out      #boxplot.stats() 함수는 리스트 형태로 여러 개의 결과값을 반환하는데 그중에서 out은 특이값을 말한다.
```
<img width="1116" alt="스크린샷 2021-09-15 오후 3 32 51" src="https://user-images.githubusercontent.com/86886489/133382475-539d6e42-b5d4-4345-b590-09f9aed4e4ea.png">  

## 특이값을 포함한 행 제거
특이값을 포함한 행을 제거할 때는 이상치를 NA로 바꾸고 NA를 포함한 행을 제거하는 방식으로 진행한다.
```R
out.val <- boxplot.stats(st$Income)$out      # 특이값 추출
st$Income[st$Income %in% out.val] <- NA      # 특이값을 NA로 대체
head(st)
newdata <- st[complete.cases(st),]           # NA가 포함된 행 제거
head(newdata)
```

## 벡터의 정렬(sort)
정렬은 데이터를 주어진 기준에 따라 크기순으로 재배열하는 과정을 말하며, 데이터 분석 과정에서 빈번하게 수행하는 작업 중의 하나이다.
```R
v1 <- c(1,7,6,8,4,2,3)
order(v1)
v1 <- sort(v1)                # 오름차순
v1
v2 <- sort(v1, decreasing=T)  # 내림차순
v2
```

## 매트릭스와 데이터프레임의 정렬
```R
head(iris)
order(iris$Sepal.Length)                         # order() 함수는 주어진 열의 값들에 대해 순서를 붙이는데, 값의 크기를 기준으로 작은 값부터 시작해서 번호를 붙인다.
iris[order(iris$Sepal.Length),]                  # 오름차순으로 정렬
iris[order(iris$Sepal.Length, decreasing=T),]    # 내림차순으로 정렬
iris.new <- iris[order(iris$Sepal.Length),]      # 정렬된 데이터를 저장
head(iris.new)
iris[order(iris$Species, -iris$Petal.Length,decreasing=T),]   # 정렬 기준이 2개
```
위의 iris[order(iris$Species, -iris$Petal.Length, decreasing=T),] 코드는 iris 데이터셋을 품종별(Species)로 내림차순으로 정렬하고, 같은 품종 내에서는 꽃잎의 길이(Petal.Length)를 기준으로 오름차순으로 정렬하는 명령문이다. iris$Petal.Length 앞에 붙은 (-)기호는 decreasing 에서 선언한 순서와 반대로 하라는 뜻으로, decreasing=T 인 경우는 오름차순의 의미가 된다. 이와 같이 order() 함수 안에 정렬 기준이 되는 열의 이름을 여러 개 나열하는 것도 가능하다.  


