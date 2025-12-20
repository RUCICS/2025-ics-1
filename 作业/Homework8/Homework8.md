# Homework 8

## T1

写一个C表达式，在下列描述的条件下产生1，其他情况产生0，假设X是int类型。代码中不能使用==或！=进行测试。

- x的任何位都等于1；
- x的任何位都等于0；
- x的最低有效字节中的位都等于1；
- x的最高有效字节中的位都等于1；

## T2

int为32位，float和double分别是32位和64位IEEE格式

```cpp
Int x =random();
Int y = random();
Int z = random();
Double dx = (double)x;
Double dy = (double)y;
Double dz = (double)z;
```

对于下面的每个C表达式，判断是否恒为1。如果是请说明原理，如果不是请举出反例。

- A. ```(float)x == (float)dx```
- B. ```dx-dy == (double)(x-y)```
- C. ```(dx+dy)+dz == dx+(dy+dz)```
- D. ```(dx*dy)*dz == dx*(dy*dz)```
- E. ```dx/dx == dz/dz```

## T3

编写如下函数，求浮点数f的绝对值|f|。如果f是NaN，那么应该直接返回f（注意NaN不要对f做任何修改）。
其中float_bits等价于unsigned，是float数字的二进制形式

```cpp
typedef unsigned float_bits;
/* Compute |f|. If f is NaN, then return f. */
float_bits float_absval (float_bits f);
```

## T4

实现如下函数，对于浮点数f，计算2.0*f。如果f是NaN，你的函数应该简单返回f。

```cpp
/* Compute 2*f. If f is NaN, return f. */
float_bits float_twice(float_bits f);
```
