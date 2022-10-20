### 选择结构

#### 一些基本知识

+ C 语言把任何**非零**和**非空**的值假定为 **true**，把**零**或 **null** 假定为 **false**

+ `if` 和 `switch` 和`A?B:C`

  ```c
  switch(表达式) // 表达式的值不能是 浮点、 long、字符串 
  {
      case 常量表达式1:语句1;break; // 常量表达式的类型要和表达式的类型一致
      case 常量表达式2:语句2;break;
      ...
      default:语句n+1;break; // 以上情况都不满足，则执行此语句
  }
  
  loop:
  	blah...
  goto loop;
  
  // 根据表达式的值，来判断从哪个case开始执行，一直到break为止
  
  switch(1){
      case 1: a = 1;
      case 2: b = 1; // 这句话也要执行
      break;
  }
  ```

+ `if`

  ```c
  if(表达式){
      执行语句;
      执行语句;
  }else{
      执行语句;
  }
  // 如果执行语句只有一条，可以省略花括号
  if(表达式)
      执行语句;
  
  if(a>b)
      c = a;
  a = b;
  b = c;

+ `continue` 和 `break`

  + `continue`，跳出当前循环，不终止循环，只可在循环中使用
  + `break`，结束整个循环，可以在循环和`switch`中使用

+ c 语言没有`<>`

+ 一条语句以 `;`

  ```c
  int a = 1, b = 2, c = 3, d = 0;
  if(a == 1 && b++ == 2){  // a == 1:true b++(2) == 2:true 
      if(b != 2 || c-- != 3){ // b != 2:true
          printf....
      }else{
          printf...
      }
  }else{
      printf...
  }
  // “短路” 现象
  // A || B A真则不执行B
  // A && B A假不执行B
  ```

+ 取本身的值只有一种情况，就是本身的时候，其他时候都取表达式的值

  ```c
  x; // 本身
  x++,++x,--x,x--; // 这些都是表达式
  
  b = a++; // 表达式的值
  
  a++;
  b = a; // 本身的值
  
  c == d++;
  
  d++; // d = d+1;
  c == d;
  ```

  

+ 逻辑运算符包含关系运算符

+ 数学表达式，关系表达式

  ```c
  0<x<10 
  // 如果式子为 数学表达式
  (x>0) && (x<10)
  // 如果式子为 关系表达式
  先判断x>0,返回结果为0或者1，再用这个结果来判断是否小于10
  (x>0)<10 
  
  x<y<z
  (y>x)&&(y<z)
  ```

+ 本身的值只有在 赋值 或者 自增自减之后才会改变

+ `'\0'` == `0`

+ 一般判断里，**其他**情况都是放在最后，是所有情况考虑后才考虑的
+ `!` 优先级高于 `==`
+ `!0` 的值为1
+ 优先级：`&&` >`||`

+ 多个运算符的时候 从左到右 先两两比较，运算后在比较之后两个运算符



### 循环结构

```c
// for
for(初始化，只在最开始执行一次; 每次循环开始判断; 每次循环结束都会执行的 ){
    blah...
}

while(表达式，循环条件，每循环一次进行一次判断){
    blah...
}

do{
    blah...
}while(表达式);
// dowhile 先执行后判断，while先判断后执行
// break，跳出循环
// continue 跳过当前循环剩余语句，直接进行下次循环

// for、while、if、else等如果没有打花括号 {}，则说明执行语句只有一条
```



#### 函数

```c
// 函数
// 返回类型 函数名（参数类型 参数名）{
//  函数体。。。。
//  返回值（return语句）
//}
double f(double x){
    return x * x + 1;
}
```

```c
// 外层次数*内层次数
// 表1 n1， 表2 n2
do{
    while(表达式1)
        A
}while(表达式2);
// （n2+1）n1

while(表达式1){
    do{
        B
    }while(表2)
}
// n1*(n2+1)

while(表1){
    A
}
// n1
do{
    
}while(表1)
// n1 + 1
```

| a=1               | b=1  |
| ----------------- | ---- |
| a-- == 1(a==0)    | 0    |
| a-- == 0(a == -1) | /    |
|                   |      |

### 数组

+ `&` ：取地址
+ 取元素：
  + `*`: 解引用（获取改地址的值）
  + `[index]`: 对于数组还可以通过下标（索引index）获取地址的值
+ 数组的首元素的地址就是数组名，**数组名是个常量**，**不能改变**，任何对数组名的赋值都是错误的
+ float a[10]; a是数组名，不能改变它的值

```c
int a[5];
a[0]; // 首元素
&a[0]; //首元素地址

a; // 也是首元素地址
*a; // 首元素
*(a+1); // 第二个元素
// 数组中地址加一，地址值加一个元素大小
a++;// error
a+1;

int a[5];
int *p = a;
p[0];
```

| int a[0] | a[1]                               | a[2] | a[3] | a[4] |
| -------- | ---------------------------------- | ---- | ---- | ---- |
| 0x001    | 0x001+(sizeof(a[1]) == 32) + 0x033 |      |      |      |
| a        | a+1                                |      |      |      |

+ strlen()，返回字符串的长度，到'\0' 为止但是不计入，sizeof要记入
+ strcpy(目标地址,源地址)，从目标地址开始，将源地址的数据逐个拷贝到目标地址，会覆盖目标地址的元素
+ strcmp(str1, str2),从首地址逐个比较
  + str1 > str2, 返回值大于零
  + <, <
  + =,  = 
+ strcat(dest, src), 连接函数**src** 所指向的字符串追加到 **dest** 所指向的字符串的**结尾** '\0'；在读取dest中\0结尾,src的首字母放在dest的\0位置
+ 以上两个函数在 string.h 头文件中



#### 数组定义

+ 大小必须明确

+ 大小必须是常量

  ```c
  int N = 208; // 变量
  #define N 208; // 常量
  ```

+ 多维数组

  ```c
  int x[4][3];
  int x[4][]; // 错的，没有给定列的大小
  int x[][3];
  // c语言中，必须给定列的大小
  ```

+ 数组赋值

  ```c
  char a[3];
  strcpy(a, "AB"); //这里占用两个字节，因为逐字符赋值到'\0'为止，所以是两个字节
  a = "AB"; // 字符串默认结尾有 '\0'结束字符，所以是三个字节
  ```

+ 指针加数组的形式

  ```c
  char *ca[3];
  // 1、首先看变量名是ca
  // 2、再往右看是[3]，说明ca是个大小为3的数组，到此右边就没有了
  // 3、再往左看是 char* 说明ca这个数组里的元素是char*的字符串
  ```

+ 计算数组的大小

  `sizeof(数组名)`，返回的是数组所占的字节数