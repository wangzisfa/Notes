# C/C++易错知识点总结：

## struct与struct*

```c
#include<stdio.h>
#include<stdlib.h>
struct arr{
  int n;  
};

int main(void) {
    struct arr name1;//可以，即声明了一个结构体变量，这个结构体变量储存在栈内存中
    struct arr *name2;//不可以，没有对该指针进行初始化定义，c中需使用malloc进行动态内存分配
    					//如下：
    struct arr *name3 = (struct arr)malloc(sizeof(struct arr));
    return 0;
}
```

## 函数未定义行为

```c
#include<stdio.h>

int buble_sort(int n; int a[]);

int main(void) {
    int a[10];
    int n;
    scanf("%d", &n);
    
    buble_sort(n, a);
    return 0;
}
```

这样的对函数定义了却并没有在主函数后编写buble_sort的行为，**属于函数的未定义行为**。这样虽然编译可以通过，但无法链接函数，部分编译器会报错如：**[Error] ld returned 1 exit status.**

