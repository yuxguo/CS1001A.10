---
title: "答案"
---

## T1

归并排序：

```c
#include <stdio.h>

int s[10010], temp[10010]; //数组⾜够⼤

void merge_sort(int l, int r);

int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
        scanf("%d", s + i);
    merge_sort(1, n);
    printf("排序后的数组： \n");
    for (int i = 1; i <= n; i++)
        printf("%d ", s[i]);
    printf("\n");
}
void merge_sort(int l, int r)
{
    // TODO: 1
    if (l == r)
        return;
    int mid = (l + r) / 2;
    merge_sort(l, mid);
    merge_sort(mid + 1, r);
    for (int i = l; i <= r; i++)
        temp[i] = s[i];

    int p1 = l, p2 = mid + 1;
    // TODO: 2
    int i = l;
    while (p1 <= mid && p2 <= r)
    {
        if (temp[p1] <= temp[p2])
            s[i++] = temp[p1++];
        else
            s[i++] = temp[p2++];
    }
    while (p1 <= mid)
        s[i++] = temp[p1++];
    while (p2 <= r)
        s[i++] = temp[p2++];
    return;
}
```

## T2

括号匹配：

```c
#include <stdio.h>
#include <string.h>
char stack[10010], s[10010];
int top = 0;
void push(char p)
{
    // TODO: 1
    stack[top++] = p;
}
void pop()
{
    // TODO: 2
    top--;
}
char get_top()
{
    //给出栈顶元素的值
    return stack[top - 1];
}
int is_empty()
{
    //返回1表示栈空， 0表示栈⾮空。
    return top == 0;
}
int check(char l, char r)
{
    //判断⼀对括号是否匹配
    return l == '(' && r == ')' || l == '[' && r == ']' || l == '{' && r == '}';
}
int main()
{
    scanf("%s", s);
    int len = strlen(s);
    int i;
    for (i = 0; i < len; i++)
    {
        char c = s[i];
        if (c == '(' || c == '[' || c == '{')
        {
            // TODO: 3
            push(c);
        }
        else
        {
            // TODO: 4
            if (!is_empty() && check(get_top(), c))
                pop();
            else
                break;
        }
    }
    // TODO: 5
    printf("%d\n", is_empty() && i == len);
}
```

## T3

汉诺塔：

```c
//注意：本代码hanoi()函数与原题目参数顺序不同
#include <stdio.h>
void hanoi(int n, char src, char mid, char dst)
{
    //函数意义：要将1到n的盘，从初始塔src，移动到⽬标塔dst，可以⽤mid塔来暂存
    // TODO: 1
    if (n == 1)
        printf("%c => %c\n", src, dst);
    else
    {
        // TODO: 2
        hanoi(n - 1, src, dst, mid);
        // TODO: 3
        printf("%c => %c\n", src, dst);
        // TODO: 4
        hanoi(n - 1, mid, src, dst);
    }
}
int main()
{
    int n;
    scanf("%d", &n);
    hanoi(n, 'A', 'B', 'C');
    return 0;
}
```
