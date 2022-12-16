### const

常类型是指使用类型修饰符**const**说明的类型，常类型的变量或对象的值是不能被更新的。

1. ***const常量***  与 ***#define宏定义常量***  的区别

>const常量具有类型，编译器可以进行安全检查，#define宏定义常量没有类型，不能进行安全检查
>
>const定义常量从汇编的角度来看，只是给出了对应的内存地址，而不是像#define一样给出的是立即数。
>
>const定义的常量在程序运行过程中只有一份拷贝，而#define定义的常量在内存中有若干个拷贝

2. const定义的变量只有类型为整数或枚举，且以常量表达式初始化时才能作为常量表达式；其他情况下它只是一个 `const` 限定的变量
3. 要使const变量能够在其他文件中访问，必须在文件中显式地指定它为extern，并且需要做初始化；非const变量默认为extern

```c++
//file1.cpp
extern const int ext=12;
//file2.cpp
#include<iostream>
extern const int ext;
int main(){
    std::cout<<ext<<std::endl;
}
------------------------------------------
// file1.cpp
int ext;
// file2.cpp
#include<iostream>

extern int ext;
int main(){
    std::cout<<(ext+10)<<std::endl;
}
```

4. 如果*const*位于`*`的左侧，则const就是用来修饰指针所指向的变量，即指针指向为常量（值不能修改）
   如果const位于`*`的右侧，*const*就是修饰指针本身，即指针本身是常量（值可以通过其他指针修改）
5. 对于非内部数据类型的输入参数，应该将“值传递”的方式改为“const 引用传递”，目的是提高效率。例如将void func(A a) 改为void func(const A &a)                  

   对于内部数据类型的输入参数，不要将“值传递”的方式改为“const 引用传递”。否则既达不到提高效率的目的，又降低了函数的可理解性。例如void func(int  x)不应该改为void func(const int &x)

6. 对于类中的const成员变量必须通过初始化列表进行初始化
7. const对象只能访问const成员函数,而非const对象可以访问任意的成员函数,包括const成员函数
8. 在一个类中，任何不会修改数据成员的函数都应该声明为const类型
9. 常量指针： const int * a   值不能改

   指针常量： int * const a: a指向的是一个地址， 不可更改，但是地址所指向的值 是可以更改的
