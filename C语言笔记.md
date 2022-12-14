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
*a+1；//a[0][1]
*(a+1); // 第二个元素a[1][0]
// 数组中地址加一，地址值加一个元素大小
a++;// error 数组名是常量不可以自增
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

+ 数组定义

  ```c
  // 定义并初始化
  int a[8] = {1, 2}; // √
  int a[8];
  a = {1, 2}; // × 数组名不能
  a[8] = {1,2}; // {} 列表初始化，只能在定义的时候用
  ```

  

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
  char a[3] = "AB"; // 字符串默认结尾有 '\0'结束字符，所以是三个字节 定义的同时进行赋值
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

### 函数

+ 数组和指针都是指针变量

```c
fun(int x,int y) // 对应一个形参都有一个类型 不可以fun(int x,y)

fun((x,y,z)(y,x,k)) //括号的个数就代表实参个数，不是看里面的具体的，此时有两个

double fun(int) //返回值是double
```

#### 函数传参

```c
int a = 5, b = 6;
int *p = &a, *q = &b;

// 函数里传入函数的参数都是副本，拷贝的

void change1(int a, int b){
    int t = a;
    a = b;
    b = t;
    // a = ?
    // b = ?
}

change1(a, b); // int tempa = a, int tempb = b; change1(tempa, tempb);
// a = 5, b = 6


void change2(int *a, int *b){
    int t = *a;
    *a = *b;
    *b = t;
}

change2(p, q); // int *tempp = p, int *tempq = q;
// p -> a, q ->b;
// tempp ->a, tempq ->b;
// 交换的是 tempp 和 tempq所指向的值，所以a, b的值交换

```

<img src="C:\Users\Qi'n'liu\AppData\Roaming\Typora\typora-user-images\image-20221115235846684.png" alt="image-20221115235846684" style="zoom:67%;" />



+ 一些易错点

```c
void func(); // 返回类型为空，无返回值
int func(); // 返回值为int时，可省略返回类型
```

#### 函数声明与定义

```c
// 函数声明，返回类型 函数名(参数列表);
returnType func(参数列表);

// 函数定义，比函数声明多了函数体
returnType func(参数列表){
    funcbody...
}

// 一个函数的调用之前，必须声明该函数
// c语言中函数内允许声明其他函数，但不可定义其他函数
```

#### 全局变量

+ 在所有函数外部定义的变量称为[全局变量（Global Variable），**它的作用域默认是从定义变量的位置到本源文件结束都有效。**

+ 未赋值，默认为零

+ staic 是静态变量， 会改变大小

+ auto 局部变量 动态分配储存空间 使用时从占用内存 如：形参

+ register 使用时才占内存，不能进行求地址运算

+ extern 静态也是全局变量 从定义到文件结束

+ 全局变量也会保留上一次结果

+ 不加staic的局部变量会重置，全局变量不会被重置类似于staic

  

### 指针

指针占用四个字节，数组指针sizeof就是元素个数*4

```c
// 指针声明，指针声明的格式为 变量类型 *变量名;
int *b; 

// 取地址,获取变量的地址
int a = 1;
int *p = &a; // & 为取地址符，获取目标变量的地址

// 解引用，获取指针所指的值
*p = 2; // 改变p所指向的值为2，也就是改变a的值为2

// 优先级
// & * 优先级高于 算数运算符，低于括号，一般括号优先级最高
*p+1; // 先*p得到所指向的值，然后这个值再加一
*(p+1); // 先p+1,指针向后移一位，指向下一个元素，然后取元素值
```

+ 指针变量

  + 常量不能取地址

  + 指针变量只能付给同类型的指针（如果不强转）

    ```c
    int a = 1;
    float b = 1.0;
    int* p; 
    // 这里*的位置可以是int *p 也可以是 int* p; p为变量名，它的类型为int* 也就是指向整型的指针 
    
    p = &a; // 正确，
    p = &b; // 错误，b的类型为float，而p所指向的类型为int，不能赋值
    ```

+ 指针是用来保存值的地址的，就跟**邮编**一样，大小长度是固定的一般两个字节。通过地址（可以理解为邮编），来找到住在这个地址上的人（也就是所指向的值）

+ 关于 `*` 

  ```c
  // * 只有在和类型一块时才表示指针声明，其他情况都表示获取指针所指向的值
  int *p; // * 在这里修饰int 表明p是一个指向int的指针
  
  *p; // 由于*没有和类型一块，所以这里是获取p所指向的值
  
  p+1; // p为指针，p+1 表示下一个元素的地址
  *(p+1); // p+1 表示下一个元素的地址，*(p+1)获取对应地址的值
  ```

+ 指针的通俗理解

  可以把指针理解为邮编，比如渝中区邮编为400000，长安区邮编为710000。

  + 首先有规定，指针变量的值只能赋给同类型的指针。这是为了防止所指向的值可能转换中会出问题

    ```c
    float a = 1.2;
    int *p;
    p = &a; // 这是错的，如果成立，那么p所指向的是一个整型，会丢失精度
    ```

  + 指针值互相赋值

    ```c
    // 对于 （指针变量的值只能赋给同类型的指针），为什么强转可以呢
    // 本质上指针就是地址大小固定的占用2字节的值，
    // 就好比邮编，渝中区和长安区的邮编都是六位，它们所占的大小是一样的，那么强制类型转换是可以的。
    // 默认不能跨变量类型赋值，可以理解为送邮件（在一个省范围内），在重庆市你用了长安区的邮编，那么这个邮件就寄不出去了
    // 可以强转赋值，可以理解为邮编有六位，理论上可以随意填写六位数，关于这六位数所组成的邮编是否合法就不得而知了，可能是外省的邮编，也可能是这个邮编在题图上就没有那个地方，所以是有风象的
    ```

  + 指针初始化

    ```c
    int *p; // 这个时候其实p的值是给这个指针变量分配的2字节内存里的原始值，就像邮编，开始给的是的随机的，不确定这个地址是不是真的存在，能不能去。p没有初始化
    int *p = &a; // p初始化，一开始就给了一个有效的地址。相当于邮编，一开始就给了一个可以去的地方的邮编。之后再改*p，也只是改变这个可以访问的地址所指向的值，如果不改变p的值（也就是改变地址了，相当于寄快递，本来是渝中区，现在改为长安区了），那么这个地址就一直可用，知道被销毁。
    ```

  + 指针与数组
  
    ```c
    char *aa[2];
    1、先看到变量名 aa
    2、向左看 是[2] 说明aa是个大小为2的数组
    3、左边完了，往右 遇到 char*
    4、说明数组中的元素为 char* 类型
    5、遇到括号就往左
    
    int (*a)[2];
    ```
  
    

**字符串与指针**

```c
字符串比较大小是以第一个字符大小为标准，与长度无关
    sizeof要计算‘\0’，主要看类型，指针类型都为4，如果定义a[8]则为8，strlen不考虑‘\0’
  char *ps[]={"aa","bb"},ps[0]表示aa的首地址，*ps[0]表示a
  char b[]="happynewyear",b+5表示newyear
  char str[]="123456"时str++为错误的 数组名不可以自增
```



#### 转义符

```c
\ddd  // 至多三位八进制数
\xdd  // 两位十六进制数
```



char toupper(char *p){

 return *p-32;

}

char c = toupper(*p);



#### 函数指针

指向函数的指针

```c
定义：
返回值类型 (*函数名)(); 

例子：
int f(int x, int y){
    return x + y;
}
int (*pf)(int x, int y) = f;
// 也可以先定义后赋值
// int (*pf)(int x, int y);
// pf = f; 

int c = (*pf)(1, 2);  // c等于3

// 怎样区分函数指针, 变量名后跟小括号就一定是函数指针
类型名* 变量名 ()
```

![image-20221116004036556](C:\Users\Qi'n'liu\AppData\Roaming\Typora\typora-user-images\image-20221116004036556.png)

声明其实就是用 (*pf) 替换掉 `f`, pf 可以是任意合法的变量名

![image-20221119001040202](C:\Users\Qi'n'liu\AppData\Roaming\Typora\typora-user-images\image-20221119001040202.png)

\*（\*(a+1）+0)
