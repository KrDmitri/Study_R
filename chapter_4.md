# 조건문, 반복문, 함수
## if-else문
```R
job.type <- 'A'
if(job.type == 'B'){
        bonus <- 200
} else {                       # 🔥주의! else는 반드시 if문의 코드블록이 끝나는 부분에 있는 }와 같은 줄에 작성해야 한다.
        bonus <- 100
}
print(bonus)
```
기본 구조는 위와 같고, 논리연산자 &(and) 와 |(or)을 사용할 수 있다.  

## ifelse문
ifelse(비교 조건, 조건이 참일 때 선택할 값, 조건이 거짓일 때 선택할 값)  

## for문
R의 for문 구조
```R
for(반복 변수 in 반복 범위) {
  반복할 명령문(들)
}
```
for문 예시
```R
for(i in 1:9){
        cat('2 *', i, '=', 2*i, '\n')     # print()와 다르게 cat()함수는 한 줄에 여러 개의 값을 출력한다.    '\n'은 줄 바꿈 특수문자
}
```

## while문
R의 while문 구조
```R
while(비교조건) {
  반복할 명령문(들)
}
```

## break와 next
break는 반복문을 중단시키는 역할, next는 반복문의 시작 지점으로 되돌아가는 역할을 한다.  

## apply() 함수
반복 작업이 필요한 경우에는 반복문을 적용하면 되는데, 반복 작업의 대상이 매트릭스나 데이터프레임의 행(row) 또는 열(column)인 경우는 for문이나 while문 대신에 apply 함수를 이용할 수 있다.  
사실 R에서 대규모의 2차원 데이터를 분석하는 경우에는 처리 속도의 문제 때문에 되도록 for문이나 while문 사용을 권장하지 않고 있다. 이 때 apply()함수를 이용하면 처리 속도를 향상시킬 수 있다.  
  
apply() 함수는 매트릭스나 데이터프레임에 있는 행들이나 열들을 하나하나 차례로 꺼내다가 평균이나 합계 구하기 등과 같은 어떤 작업을 수행하고자 할 때 유용하게 사용할 수 있다.  
apply() 함수의 문법
```R
apply(데이터셋, 행/열방향 지정, 적용 함수)      # 행방향 작업의 경우 1, 열방향 작업의 경우 2를 지정
```

## apply() 함수의 적용
```R
apply(iris[,1:4], 1, mean)      # row 방향으로 함수 적용
apply(iris[,1:4], 2, mean)      # col 방향으로 함수 적용
```

## 사용자 정의 함수 만들기
```R
함수명 <- function(매개변수 목록) {
  실행할 명령문(들)
  return(함수의 실행 결과)
}
```
예시 1
```R
mymax <- function(x,y) {
        num.max <- x
        if(y > x){
                num.max <- y
        }
        return(num.max)
}

mymax(10,15)
a <- mymax(20,15)
b <- mymax(31,45)
print(a+b)
```
## 함수가 반환하는 결과값이 여러 개일 때의 처리
list()함수를 이용
```R
myfunc <- function(x,y) {
        val.sum <- x+y
        val.mul <- x*y
        return(list(sum=val.sum, mul=val.mul))
}

result <- myfunc(5,8)
s <- result$sum                 # $접근법 활용
m <- result$mul
cat('5+8=',s,'\n')
cat('5*8=',m,'\n')
```

## 사용자 정의 함수의 저장 및 호출
<img width="312" alt="스크린샷 2021-09-12 오후 6 23 27" src="https://user-images.githubusercontent.com/86886489/132982255-16c7a1e7-0fe3-48f4-98d3-007f69f5b127.png">
```R
setwd("/Users/joseongbeom/Devspace/R/source/Ch04")      # myfunc.R이 저장된 폴더
source("myfunc.R")                                      # myfunc.R 안에 있는 함수 실행

a <- mydiv(20,4)
b <- mydiv(30,4)
a+b
mydiv(mydiv(20,2),5)
```
