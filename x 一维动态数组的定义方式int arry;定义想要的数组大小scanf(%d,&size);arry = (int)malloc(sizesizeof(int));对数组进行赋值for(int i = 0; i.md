```c
//一维动态数组的定义方式
int *arry;
//定义想要的数组大小
scanf("%d",&size);

arry = (int*)malloc(size*sizeof(int));
//对数组进行赋值
for(int i = 0; i < size; i++){
    arry[i] = i
}
//输出数组内元素
for(int i = 0; i < size; i++){
    printf("%d",arry[i]);
}
//释放对arry所分配的内存块
free(arry);
```

