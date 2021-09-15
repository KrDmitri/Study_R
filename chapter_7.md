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

## ⚠️ NA 값이 많은 데이터 처리
어떤 데이터셋은 NA 값을 포함한 행이 많아 이를 모두 제거하면 남는 것이 별로 없어서 데이터를 분석하기 어려운 경우가 있다. 이런 경우에 만약 NA 값이 특정 열에 몰려 있다면 그 열은 제외하고 데이터를 분석한다. NA값이 여러 열에 흩어져 있는 경우는 NA 값을 적당한 값으로 추정하여 대체한 후 분석할 수 있다.

## 특이값의 개념



