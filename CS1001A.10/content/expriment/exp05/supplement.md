---
title: "补充材料- C语言 rand 函数的使用"
math: true
---

```
#include <stdlib.h>
#include <time.h>
#include <stdio.h>
int main(){
    srand((int)time(NULL));
    int a=rand();//生成0-32767之间的整数
}
```