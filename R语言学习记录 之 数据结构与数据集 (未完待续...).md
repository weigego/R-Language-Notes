R语言学习记录 之 数据结构与数据集--Day2

Hi, what’s up. 我是R语言小白一枚。近期参加了一个R语言学习小组，使用的学习材料为：https://rlearning.netlify.app/task-01.html#%E5%90%91%E9%87%8Fvector。我也将开始使用CSDN记录每次课的学习笔记和遇到的问题，希望能对您有所帮助~

# 数据结构与数据集
## 常见的算术运算 (Arithmetic Operations)
### 加 (plus)
```r
e.g.
> 1+2
[1] 3
```
### 减 (subtract)
```r
e.g.
> 1-1
[1] 0
```
### 乘 (multiply)
```r
e.g.
> 1*2
[1] 2
```
### 除 (divide)
```r
e.g.
> 1/2
[1] 0.5
> 1/3
[1] 0.3333333
```
### 幂 (power)
```r
e.g.
> 2^4
[1] 16
> 2^10
[1] 1024
> 2^1000
[1] 1.071509e+301
> 2^10000
[1] Inf 
```
### 取余 (remainder)
```r
e.g.
> 3%2
Error: unexpected input in "3%2"
> 3%%2
[1] 1
```
### 开平方根 (square root)
```r
e.g.
> sqrt(4)
[1] 2
> sqrt(2)
[1] 1.414214
```

## 赋值运算 (assignment)
var <- num 作用上等价于 var = num 、 num -> var
（```<-```的快捷键是 ```Alt```+ ```-```)
```r
e.g.
> x<-3
> x
[1] 3
> y=4 
> y
[1] 4
> x->y
> y
[1] 3
> x
[1] 3
```
## 函数 (function)
如何定义函数：
```r
函数名 <- function (参数){
	函数体
}
```

如何调用函数：
```r
函数名（参数）
```
**Notes**: 函数有多个可选参数的时候，建议输入参数的时候使用等号=明确函数名称。

e.g. 下面定义一个名为addone的函数，函数有一参为x，其默认值为x=0。
```r
addone <- function( x = 0 ){ #x的默认值为0
 x+1 #传入的x做运算x+1
}  #函数运行结束后输出数值x+1
```
运行看看：
```r
> addone
function( x = 0 ){
    x+1
}
```
```r
> addone()  #没有传参时，默认x=0（见addone函数的定义）
[1] 1 
```
```r
> addone(22)
[1] 23
```
```r
> x=3
> addone(x)
[1] 4
```
完成了计算记得储存结果！
```r
y <- 42
y_new <- addone(y)
```
## 循环（loop）
除了for, while之外，还有repeat。

**for循环**
例子：
```r
x <- 0
for(i in 1:3){
    x <- x + i
    print(x)
}
```
```r
[1] 1
[1] 3
[1] 6
```
**while循环**
例子：
```r
> cnt <- 0
> while(cnt<10){
+ print(v)
+ cnt <- cnt+1
+ }
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
[1] "my"  "big" "dio"
```

**repeat循环**
例子：求 $0^{2}+1^{2}+...+10^{2}$：
```r
> n <- 0
> sum <- 0
> repeat{ 
+ if (n>10) break
+ sum <- sum + n
+ n <- n+1
+ }
> sum
[1] 55
```
## 管道（pipe）
e.g.
调用自定义的函数addone, 将值传给函数addtwo进行下一步运算, addthree接受addtwo的值进行运算。
**方法1：函数的直接嵌套**
```r
#定义addone
> addone <- function(x) x+1 
> addone
function(x) x+1
#定义addtwo
> addtwo <- function(x) x+2
#定义addthree
> addthree <- function(x) x+3
```
```
> x <- 0
> addthree(addtwo(addone(x)))
[1] 6
```
以上函数的执行顺序是由内到外，但是这导致代码的可读性差。

**方法2：管道**
`%>%` 是符号函数进行方法链的操作，意思是将上一步的运算结果作为下一步的输入参数，可以把它视为管道。

```r
library(magrittr) #需要调用包tidyverse 或者 magrittr
> x %>%
+     addone() %>%
+     addtwo() %>%
+     addthree()
```
```r
[1] 6
```
 由此，”从内到外“变为”从上到下，从左到右“，可读性提升。
管道符号的具体使用规则详见`?%>%`
# 数据类型 (Data Type)
## 1. 基本数据类型
R中有五种基础数据类型：三个数值型、一个逻辑型和一个字符型

**数值型**：实数数值型数据（double）、整数类型（integer）和复数类型（complex）
```r
> a <- 12.345
> typeof(a)
[1] "double"
```
```r
> b <-  12 
> typeof(b)
[1] "double" #注意，这里仍未double型

> b <-  12L
> typeof(b)
[1] "integer" #整数末尾加L，代表数据类型为整数！！
```
```r
> c <- 2+3i
> c
[1] 2+3i
> typeof(c)
[1] "complex"
> 
```
**逻辑型**：TRUE / T 和 FALSE / F
```r
> 2>1
[1] TRUE
> T #缩写也可以哦~
[1] TRUE
> F
[1] FALSE
```
**Notes**: TRUE、FALSE全大写！！
```r
> true
Error: object 'true' not found
```
拓展：逻辑算符
and `&`, or `|`, not `!` , etc.
```r
> 1>2 &1>0
[1] FALSE

> 1>2 |1>0
[1] TRUE

> !1>2  #(相当于!(1>2), 因为>优先级大于!)
[1] TRUE

> !1
[1] FALSE

> !0
[1] TRUE

> !-1 #从这里也可以看出，非零数值代表TRUE
[1] FALSE
```

**字符型**：任何带引号的单个数值、单个字符串/字符
```r
> c<- 1
> typeof(c)
[1] "double"
> c<- '1'
> typeof(c)
[1] "character"
```
```r
> c <- 'TRUE'
> typeof(c)
[1] "character"
> typeof(TRUE)
[1] "logical"
```
```r
> str <- "my big dio"
> str
[1] "my big dio"
> typeof(str)
[1] "character"
```
多个字符串的情况：
```r
> str <- c('my','big','dio') #实际上这是一个向量，见下方 2.向量 的内容
> str
[1] "my"  "big" "dio"
> typeof(str)
[1] "character"
```
R中的单引号（'）和双引号（"）是等效的，但是使用时要遵循匹配原则。
```r
> str <- c('"OMG" is Oh my god')
> str
[1] "\"OMG\" is Oh my god"
```
题外话：C语言里，单双引号使用起来不同。
## 2. 向量（vector）
这里只讨论基础向量类型（atomic vector）。
向量是由一组**相同类型的值**组成的一维序列。
根据值的类型不同，我们会有不同类型的向量：数值、逻辑和字符型的向量类型（对应于前面的数值、逻辑和字符型的基础数据类型）。
如何构建向量：使用函数`c()`来构建向量。
```r
> vec_num <- c(1,2,3)
> vec_num
[1] 1 2 3
> typeof(vec_num)
[1] "double"
```
```r
> vec_num2 <- c(1L,2L,3L)
> vec_num2
[1] 1 2 3
> typeof(vec_num2)
[1] "integer"
```
```r
> vec_cha <-  c('a','b','c')
> vec_cha
[1] "a" "b" "c"
```
```r
> vec_mix <- c(1,'a',2) 
> vec_mix
[1] "1" "a" "2"
> typeof(vec_mix)
[1] "character" #自动将数值型转化为字符型了！！！
```
```r
> vec_logic = c(TRUE,FALSE)
> vec_logic
[1]  TRUE FALSE
> typeof(vec_logic)
[1] "logical"
> !vec_logic
[1] FALSE  TRUE
```
可以进行向量上的运算，而不用一个一个值地单独去计算。
```r
> vec_num1 <- c(1,2,3)
> vec_num2 <- c(3,2,1)
> vec_num1+vec_num2 # 等同于 c(1 + 3, 2 + 5, 3 + 6)
[1] 4 4 4
```
注意: 在R语言中`+`不能直接用于字符串的拼接，别和python混淆。
```r
> vec_cha1 <- c('hello','R')
> vec_cha2 <- c('Language','!')
> vec_cha1
[1] "hello" "R"    
> vec_cha2
[1] "Language" "!"       
> vec_cha1 + vec_cha1
Error in vec_cha1 + vec_cha1 : non-numeric argument to binary operator

> 'hello'+'you'
Error in "hello" + "you" : non-numeric argument to binary operator
```
R语言中有作用于向量的函数，可以计算相应的统计量。比如求和的sum、求方差的var、平均值的mean等：
```r
> vec_num <- c(2,3,4)
> sum(vec_num)
[1] 9
> var(vec_num)
[1] 1
> mean(vec_num)
[1] 3
```
### 因子
向量可由基础数据类型组成，还可由因子构成，需要使用函数factor和c组合来创建。
先看一个例子：
```r
> vec_fac <-  c('male','female','male','female')
> vec_fac
[1] "male"   "female" "male"   "female"

> vec_fac <-  factor(c('male','female','male','female'))
> vec_fac
[1] male   female male   female
Levels: female male  #四个元素中只含有两个独特值
```
由此可看出，因子向量和字符向量都是由一连串的带引号的字符串组成的。差别在于，在因子向量中，因子的独特值(levels)是有限个数的，因子向量正是由这些有限个数的独特值构成。

使用函数levels() 可查看因子向量的独特值
```r
> levels(vec_fac)
[1] "female" "male"  
```
如何创建一个元素之间具有内在顺序的因子向量？
使用函数ordered或者factor里的ordered = TRUE参数（argument）创造一个有内在顺序的因子向量，内在顺序可以用levels参数来手动设定：
```r
> edu <- ordered(
  c('high school','primary school','kindergarten',
    'high school','middle school'),
  levels=c('kindergarten','primary school','middle school','high school')
)
> edu
[1] high school    primary school kindergarten   high school    middle school 
Levels: kindergarten < primary school < middle school < high school
```
或者
```r
> edu <- factor(
  c("kindergarten", "primary school", "middle school", 
    "primary school", "middle school", "kindergarten"),
  ordered = TRUE, 
  levels = c("kindergarten", "primary school", "middle school")
)
> edu
[1] high school    primary school kindergarten   high school    middle school 
Levels: kindergarten < primary school < middle school < high school
> 
```
拓展：R 把因子向量当作整数型数值向量来对待。这也就意味着用因子向量替代字符向量可以剩下很多字节。

未完待续......
2021/08/19

#### 数值之间的转换
#### 向量命名
#### 访问向量的子集
## 3. 特殊数据类型
### 日期
### 时间序列（ts）
# 4. 多维数据类型
二维甚至多于二维的数据类型。
### 矩阵
#### 矩阵命名
#### 访问矩阵子集
### 列表
#### 访问子列表

#### 列表命名

### 数据表

#### 访问数据表内容

## 读写数据

### 内置数据集
### 表格类型的数据
