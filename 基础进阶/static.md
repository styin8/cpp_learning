### static

1. 当变量声明为static时，空间**将在程序的生命周期内分配**。即使多次调用该函数，静态变量的空间也**只分配一次**，前一次调用中的变量值通过下一次函数调用传递。即静态变量只会初始化一次，比如：

   ```c++
   #include <iostream> 
   #include <string> 
   using namespace std; 
   void demo() 
   { 
   	static int count = 0; 
   	cout << count << " "; 
   	count++; 
   } 
   
   int main() 
   { 
   	for (int i=0; i<5; i++)	 
   		demo(); 
   	return 0; 
   } 
   
   //返回值是0 1 2 3 4
   // count只初始化了一次
   ```

2. 类中的静态变量应由用户在类外使用类名和范围解析运算符显式初始化

   ```c++
   #include<iostream> 
   using namespace std; 
   class Apple 
   { 
   public: 
   	static int i = 1; 
   	
   	Apple(){}; 
   }; 
   
   //int Apple::i = 1; 
   
   int main() 
   { 
   	Apple obj; 
   	cout << obj.i; 
   } 
   //在类内初始化会报错[Error] ISO C++ forbids in-class initialization of non-const static member 'Apple::i'
   //只能使用上面注释的语句初始化
   ```

3. 类对象为静态

   当类对象为静态时，那么类的析构函数会在程序执行完成后才会被调用，这是因为静态对象的范围是贯穿程序的生命周期。

4. 静态成员函数仅访问静态数据成员或其他静态成员函数，它们无法访问类的非静态数据成员或成员函数