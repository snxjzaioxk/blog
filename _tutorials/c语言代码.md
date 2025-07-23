---
layout: post
title: "代码"
lesson: 2
category: c
---

# 输出a++和++a

```
#include<stdio.h>
int main(){
    int a = 10;
    printf("a++=%d\n a=%d\n",a++,a);//输出a++的值和a的值
    printf("++a=%d\n a=%d\n",++a,a);//输出++a的值和a的值
    return 0;
}
```



# 交换两个变量

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

# 输出十六进制

```
int main(){
    int x;
    printf("请输入一个整数：");
    scanf("%d",&x);
    printf("十六进制为；0x%x",x);//输出十六进制的数
    return 0;

}
```

# 计算时间差

```
int main(){
    int huor1,minute1;
    int huor2,minute2;//定义接收时间分钟

    printf("请输入第一个时间（小时 分钟）：");
    
    scanf("%d %d",&huor1,&minute1);//接收第一个时间 
    printf("请输入第二个时间（小时 分钟）：");
    scanf("%d %d",&huor2,&minute2);//接收第二个时间
    int total1 = huor1 * 60 + minute1; //将第一个时间转换为分钟
    int total2 = huor2 * 60 + minute2; //将第二个
    int diff = total2 - total1; //计算时间差
    if (diff < 0) {
        diff += 24 * 60; //如果时间差为负数，说明跨天了，增加24小时的分钟数
    }
    int diff_huor = diff / 60; //计算小时
    int diff_minute = diff % 60; //计算分钟
    printf("时间差为：%d小时 %d分钟\n", diff_huor, diff_minute); //输出时间差

}

```

# while和do-while求平均数

```
#include<stdio.h>
int main(){
    int num;
    int sum ;
    int count = 0;
         scanf("%d",&num);
    while(num != -1){
   
        sum += num; // 累加输入的数字
        count++; // 计数输入的数字
        scanf("%d",&num);
    }
    printf("次数为%d\n平均数为%.f\n",count,1.0*sum/count);
    return 0;
}



#include<stdio.h>
int main(){
    int num;
    int count = 0;
    int sum = 0;
    do{
        scanf("%d",&num);
        if(num != -1){
            sum +=num;
            count++;
        }
    }while(num != -1);
        printf("输入的次数为%d\n平均数为%.f",count,1.0*sum/count);
    return 0;
}
```

# 猜数字游戏

```
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

int main(){
    srand(time(0));//设置随机数种子为当前时间
    int num = rand()%100;//随机生成0-99之间的整数
    int a = 0;
    int count = 0;
    do{
        printf("请输入0-99之间的整数：");
        scanf("%d",&a);
        count++;
        if(a > num){
            printf("你输入的数字大了\n");
        }
        else if(a < num){
            printf("你输入的数字小了\n");
        }
        else{
            printf("恭喜你答对了，你一共输入了%d次\n",count);
        }
    }while(num != a);
    return 0;
}
```

# 整数逆序

```

// //逆序输入 如果末尾为0 也输出
// #include<stdio.h>
// int main(){
//     int x,digit;
//     int ret = 0;
//     scanf("%d",&x);
//     while(x > 0){
//         digit=x%10;//取最后一位数字
//         printf("%d",digit);//输出最后一位
//         ret =ret*10 + digit;//累加最后一位数字
//         x/=10;//去掉最后一位
//     }
//     return 0;
// }



// // 逆序输入 如果末尾为0 不输出
// #include<stdio.h>
// int main(){
//     int x,digit;
//     int ret = 0;
//     scanf("%d",&x);
//     while(x > 0){
//         digit = x%10;
//         ret = ret*10 +digit;
//         x/=10;
//     }
//     printf("%d",ret);
//     return 0;s
```

# for循环

```
// #include<stdio.h>
// int main(){
//     int n;
//     int fac = 1;
//     scanf("%d",&n);
//     for(int i = 1; i <= n; i++){
//     fac*=i;
//     }
//     printf("%d的阶乘为%d\n",n,fac);
//     return 0;
// }


////优化 使用i-- 省略一个变量
// #include<stdio.h>
// int main(){
//     int fac = 1;
//     int n = 0;
//     scanf("%d", &n);
//     for(n;n>1;n--){
//         fac *= n;
//     }
//     printf("%d\n",fac);
//     return 0;
// }
```

