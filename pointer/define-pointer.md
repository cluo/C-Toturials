# 指针的定义与使用

##指针的定义

在程序当中，我们使用`*`表示指向。指针变量的定义为：

指向单元的数据类型 *指针变量名;

```
int *intPointer;      // 指向int变量的指针intPointer
float *floatPointer;  // 指向float变量的指针floatPointer
char *charPointer;    // 指向char变量的指针charPointer

```

虽然，指针可以指向不同类型的变量，如以上的`intPointer`、`floatPointer`、`charPointer`，但他们所占的内存空间与指向变量的类型所占空间无关。意思是，`intPointer`、`floatPointer`、`charPointer`所占的内存都是8个字节（64位下）。

**既然无论什么类型的指针都是占8个字节，那为什么还要分类型呢？**

简单的讲，是为了告诉编译器，应该读几个字节。可以看看这个例子：

```
int a = 1;
char b = 2;

int *p = &b;

printf("%d", *p);

```

##指针的初始化与赋值

<font color=red>没有具体指向的指针不能使用</font>。刚定义的指针，还没有初值，这时系统会随便指向一块地址，如果这块地址正被其他程序所占用，那么操作这块地址，可能会造成系统混乱。所以，定义指针以后，最好有一个初始化的好习惯，避免<font color=red>野指针异常</font>。

```
int *p = NULL; // 定义指针变量以后，初始化指向为NULL(未指向任何一块地址)

```

###&取地址符

如果需要指向某一个变量，那首先需要得到这个变量的地址。

```
int a = 10;
int *p = &a; // 注意*p的类型要与a的类型一致

```

###指针的赋值

- 定义指针变量，并给初始值，这一步叫做<font color=red>初始化</font>。
- 定义以后，在其他地方给值，这一步叫做<font color=red>赋值</font>。

```
int a = 10;
int *p = NULL; // 定义指针变量，并初始化为NULL
p = &a;        // 将a的地址赋值给，注意：这里的p没有*

```

##指针的使用

这里有一个比较容易混淆的知识点`*`。

- 指针变量在定义时，需要使用`int *p;`；
- 但当定义以后，使用`p`来进行指针变量的访问；
- 定义以后，使用`*p`中的`*`则表示指针运算符，将对这块地址中存储的值，进行间接访问。

举个例子：

```
int a = 10;            // 定义变量a，并初始为10
int *p = NULL;         // 定义指针变量p，并初始为NULL
p = &a;                // 将a的地址赋值给p
printf("a = %d", *p);  // *p将间接访问p指向地址的值，即10

```

以下例子是<font color=red>错误</font>的：

```
int *p = NULL;
p = 10;         // 未加*的指针变量p表示的是地址，不能给地址赋值为10

```
```
int *p = NULL;
*p = 10;        // p未指向任何一块地址，不能进行赋值

```

```
int a = 10;
int *p = a;     // 在初始的时候，*p表示地址，不能直接将变量a的值给它，应修改为*p = &a;

```

##通过指针，修改变量的值

先来看看以前的实现方式：

```
int a = 10;
a = 11;

```

通知指针，进行间接访问的方式：

```
int a = 10;
int *p = &a;

*p = 11;

```

##指针的运算

下面的例子为实现一个加法运算：

```
int a = 5, b = 4;
printf("%d\n", a + b);  // 普通写法

int *p = &a, *q = &b;
printf("%d\n", *p + *q); // 使用指针，间接访问进行计算

```
