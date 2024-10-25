考虑以下代码：
```cpp
#include <iostream>
int main()
{
    std::cout << abs(-1.5) << '\n';
    std::cout << std::abs(-1.5) << '\n';
}
```
在linux下通过g++ (GCC) 14.2.1 编译或在windows下通过mingw11.2编译，运行结果：
```
1
1.5
```
在windows下通过vs2022编译，运行结果：
```
1.5
1.5
```
在linux下，通过IDE查找abs相关定义可知（mingw同理）：
abs定义在stdlib.h中，为C语言函数。仅有一个声明`int abs( int n );`（C语言不支持函数重载）
std::abs定义在std_abs.h中，为C++函数。有多个重载，支持整形和浮点型。
第一个cout中abs(-1.5)将-1.5隐式转化成-1后再取绝对值，结果为1。
那为什么通过vs2022编译的程序第一行输出为1.5呢？
在vs2022中将abs转到定义文件（cstdlib）可知，abs的浮点型重载直接被定义在了全局命名空间中。后续使用：
```cpp
namespace std {
using ::abs;
}
```
将全局命名空间下的`abs`函数引入`std`命名空间。
还有坑，考虑如下代码：
```cpp
#include<stdlib.h>
int main()
{
    abs(-1.5);
}
```
以上代码在vs2022中直接编译不通过（对重载函数的调用不明确），linux g++及mingw编译正常（仅有int作为输入参数的函数定义，没有二义性的隐式转换）。
为什么？在Windows Kits的stdlib.h中（被vs2022编译器调用），有如下重载：
```cpp
#ifdef __cplusplus
extern "C++"
{
    inline long abs(long const _X) throw()
    {
        return labs(_X);
    }

    inline long long abs(long long const _X) throw()
    {
        return llabs(_X);
    }
	...
}
#endif // __cplusplus
```
猜测是为了跟cstdlib中的`namespace std {using ::abs;}`打配合，在全局命名空间下定义输入参数为long及long long的重载。
## 对以上现象看法：
根据cppreference文档，全局命名空间下的`abs`应该仅有`int abs( int n );`这一声明。
https://en.cppreference.com/w/c/numeric/math/abs
全局命名空间下的其它函数重载可以被视为vs的非标准扩展。
## 结论：
对于非msvc编译器：使用abs函数处理非int值时必须加上std::限定，建议对所有类型的处理加上std::限定，固定使用std::abs。或使用对应类型的C语言函数（太繁琐了没必要，又容易错）
对于msvc编译器：建议同上。不要过于依赖编译器特性，不能保证所有版本msvc编译器均有以上特性且日后不发生变化。同时基于代码的可移植性考虑。
