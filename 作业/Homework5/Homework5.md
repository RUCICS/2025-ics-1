## Homework5

姓名 学号

---

### Q1

##### Consider the following program:

```c
#define LEN 10
int a[LEN][LEN];
void f(void)
{
  int i, j;
  for (i = 0; i < LEN; i++)
    for (j = 0; j < LEN; j++)
    {
      a[i][j] = i * LEN + j;
    }
}
```

##### Suppose the address of a is 0x10000000. After the function f() finished, fill the following table (if you don’t know the value, please write NONE):

#### Answer1

|     Place     |           Value           |
| :-----------: | :-----------------------: |
|     %eax      |        0x10000000         |
|     %ecx      |            22             |
|  $0x10000004  |                           |
|  0x10000012   |                           |
|  0xFFFFFFF8   |                           |
| (%eax,%ecx,8) |                           |



### Q2

##### Fill the blanks of the C program:

```c
int dw_loop(int x, int y, int n)
{
  do
  {
    /* */
  } while (/* */);
  return x;
}
```

##### The assembly code is as follows:

```nasm
  x@%ebp+8, y@%ebp+12, n@%ebp+16

  movl 8(%ebp), %eax // x
  movl 12(%ebp), %ecx // y
  movl 16(%ebp), %edx // n
.L2:
  addl %edx, %eax
  imull %edx, %ecx
  subl $1, %edx
  testl %edx, %edx
  jle  .L5
  cmpl %edx, %ecx
  jl .L2
.L5:
```

#### Answer2


### Q3

##### After ICS class, Barathrum has written a function like below:

```c
int cmov_complex(int x, int y)
{
  return x < y ? x * y : (x + y) * y;
}
```

##### (1). Please write down the corresponding assembly code by using conditional move operations.

#### Answer3(1)



##### (2). When Barathrum compiles it with gcc, he finds that there’s no cmov at all in the assembly code! Please explain why gcc doesn’t use conditional move operations in this case.

#### Answer3(2)



### Q4

Translate the following switch statements into assembly using jump table.

```c
  int x = <some value>;
  int result = 0;
  switch (x)
  {
  case 24:
    result = x + x;
    break;
  case 27:
  case 28:
    result = x + 10;
    break;
  case 26:
    result = x * 2;
  // Notice: there is no break here!
  case 29:
  case 30:
    result = result + 5;
    break;
  default:
    result = 3;
    break;
  }
```

#### Answer4
