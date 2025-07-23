---
layout: post
title: "c语言笔记"
lesson: 1
category: c
---

# c语言笔记

## 变量和常量

### 变量

可以改变的值

### 常量

1.即数字不会改变的值

2.用const来定义常量  也就是变量不变



## 运算符优先级

### 单目运算符

+单目不变 自右向左

举例 a*+b

-单目取负 自右向坐

举例a*-b

### 双目运算符

+-*/%

自左向右

### 赋值运算符

=

自右向左

## 交换两个变量

```
#include<stdio.h>
int main(){
    int a,b,tem;
    scanf("%d %d",&a,&b);//输出a，b
    tem =a;//将a的值赋给tem
    a = b;//将b的值赋给a
    b = tem;//将tem的值赋给b
    printf("%d %d",a,b);//输出交换后的a，b
    return 0;
}
```

## 增增减减运算符

a++ 是a加1以前的结果

++a是a加1以后的结果

```
#include<stdio.h>
int main(){
    int a = 10;
    printf("a++=%d\n a=%d\n",a++,a);//输出a++的值和a的值
    printf("++a=%d\n a=%d\n",++a,a);//输出++a的值和a的值
    return 0;
}
```

输出结果

```
a++=10//a++ 是a加1以前的结果
 a=11//a为11
++a=12//在a=11的基础上  ++a是a加1以后的结果
 a=12
```

## 二分法

猜数字游戏
