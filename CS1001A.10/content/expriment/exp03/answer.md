---
title: "答案"
---
## P39-T6

代码如下（未实现输入输出的提示语）

``` c
#include <stdio.h>
#include <math.h>
#define EPS 1e-6

void sort3(float *);
int triangle_type(float *);
float triangle_area(float *);
int feq(float, float);

int main(void) {
    float line[3];
    float area = -1.0;
    int type;
    scanf("%f%f%f", &line[0], &line[1], &line[2]);
    sort3(line);
    for (int i = 0; i < 3; ++i) {
        printf("%f, ", line[i]);
    }
    type = triangle_type(line);
    if (type) {
        area = triangle_area(line);
    }
    printf("%d, %f", type, area);
    return 0;
}

int feq(float a, float b) {
    return fabs(a - b) < EPS;
}

void sort3(float *line) {
    float tmp;
    for (int i = 0; i < 3; ++i) {
        for (int j = i + 1; j < 3; ++j) {
            if (line[i] > line[j]) {
                tmp = line[i];
                line[i] = line[j];
                line[j] = tmp;
            }
        }
    }
}
int triangle_type(float *line) {
    if (!(line[0] + line[1] > line[2])) {
        return 0; // 不构成三角形
    } else {
        if (feq(line[0], line[1]) && (feq(line[2], line[1])) {
            return 1; // 等边
        } else if (feq(line[0], line[1]) || (feq(line[2], line[1])) {
            return 2; // 等腰
        } else if (fabs(line[2] * line[2] - line[1] * line[1] - line[0] * line[0]) < EPS) {
            return 3; // 直角
        } else {
            return 4; //一般
        }
    }
}
float triangle_area(float *line) {
    float s = 1.0 / 2 * (line[0] + line[1] + line[2]);
    return sqrt(s * (s - line[0]) * (s - line[1]) * (s - line[2]));
}
```

注意：

- 可以使用模块化程序设计的思路，将每个模块独立实现为一个函数
- 可以先将3边排序，有助于减少后续处理的判断次数
- 注意等边三角形是特殊的等腰三角形，所以在判断时等边三角形对应的if分支要先于等腰三角形
- 注意浮点数不能直接用等号进行比较，需要在一定的误差范围内就认为相等`EPS = 1e-6`

## P40-T7

### 整数输入

使用switch判断可以统一除以某个证书，根据剩余的结果来使用switch跳转，本题中可以对成绩除以5，结果为20、19对应GPA4.3，18对应4，17对应3.7

### 浮点输入

较为简单，略

## P40-T1

代码如下（未实现输入输出的提示语）：

``` c
#include <stdio.h>
#define MAX 100
#define EPS 1e-6

int main(void) {
    float num_f;
    int num_i;
    int a1[MAX], a2[MAX];
    scanf("%f", &num_f);
    if (num_f < 0) {
        num_f = -num_f;
        printf("-");
    }
    num_i = (int )num_f;
    int i;
    // 整数部分模2取余
    for (i = 0; i < MAX && num_i != 0; ++i) {
        a1[i] = num_i % 2;
        num_i /= 2;
    }
    for (; i > 0; --i) {
        printf("%d", a1[i - 1]);
    }
    num_f = num_f - (int )num_f;
    if (num_f > EPS) {
        printf(".");
        // 小数部分乘2取整
        for (i = 0; i < MAX && num_f > EPS; ++i) {
            a2[i] = (int )(num_f * 2);
            num_f = num_f * 2 - (int )(num_f * 2);
        }
        for (int j = 0; j < i; ++j) {
            printf("%d", a2[j]);
        }
    }
    return 0;
}
```

注意：

- 数组下标访问不要越界

## P41-T2

代码如下（未实现输入输出的提示语）：

``` c
#include <stdio.h>

int main(void) {
    int a, b;
    scanf("%d%d", &a, &b);
    for (int i = a; i > 1; --i) {
        if (!(a % i) && !(b % i)) {
            a /= i;
            b /= i;
        }
    }
    printf("%d, %d", a, b);
}
```

从分子到2依次尝试即可

## P41-T3

较为简单，略（只需要注意数组访问不要越界）

## 附加题

代码如下：

``` c
#include <stdio.h>

float int2float(int);

int main(int argc, char *argv[])
{
    int i;
    scanf("%d", &i);
    printf("Int number: %d\n", i);
    printf("Converted number: %f\n", int2float(i));
    return 0;
}

float int2float(int i)
{
    int sign;
    int exp;
    int frac;
    int result;
    if (i > 0) {
        sign = 0 << 31;
    } else if (i < 0) {
        sign = 1 << 31;
        i = -i;
    } else {
        result = 0;
        return *(float *)(&result);
    }
    exp = 0;
    for (int tmp = i; tmp != 1; tmp /= 2) {
        exp++; // 计算该整数的二进制科学计数法的指数大小
    }
    frac = i & ~((0x1) << (exp)); // 整数只会产生规约形式的浮点数，需要把最高位的1置0
    frac <<= (23 - exp); // 注意左移的位数与exp相关
    exp += 127;
    exp <<= 23;
    result = (sign | exp | frac); // 使用按位或运算拼接三部分
    return *(float *)(&result);
}
```

