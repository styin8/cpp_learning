### this

1. this作用域是在类内部，当在类的非静态成员函数中访问类的非静态成员的时候，编译器会自动将对象本身的地址作为一个隐含参数传递给函数。也就是说，即使你没有写上this指针，编译器在编译的时候也是加上this的，它作为非静态成员函数的隐含形参，对各成员的访问均通过this进行。
2. 在类的非静态成员函数中返回类对象本身的时候，直接使用 return *this。
3. 当参数与成员变量名相同时，如this->n = n
4. this在成员函数的开始执行前构造，在成员的执行结束后清除。



### inline

1. 类中定义了的函数是隐式内联函数,声明要想成为内联函数，必须在实现处(定义处)加inline关键字

2. inline要起作用,inline要与函数定义放在一起,inline是一种“用于实现的关键字,而不是用于声明的关键字

3. 编译器对 inline 函数的处理步骤

   > 将 inline 函数体复制到 inline 函数调用点处；
   >
   > 为所用 inline 函数中的局部变量分配内存空间；
   >
   > 将 inline 函数的的输入参数和返回值映射到调用方法的局部变量空间中；

4. 内联能提高函数效率，但并不是所有的函数都定义成内联函数！内联是以代码膨胀(复制)为代价，仅仅省去了函数调用的开销，从而提高函数的执行效率。

   > 如果执行函数体内代码的时间相比于函数调用的开销较大，那么效率的收益会更少
   >
   > 每一处内联函数的调用都要复制代码，将使程序的总代码量增大，消耗更多的内存空间

5. 虚函数可以是内联函数，内联是可以修饰虚函数的，但是当虚函数表现多态性的时候不能内联。因为内联是在编译期进行编译器内联，而虚函数的多态性在运行期，编译器无法知道运行期调用哪个代码，因此虚函数表现为多态性时（运行期）不可以内联。