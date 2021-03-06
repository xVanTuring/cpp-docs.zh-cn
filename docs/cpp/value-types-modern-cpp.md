---
title: 值类型（现代 C++）
ms.date: 05/07/2019
ms.topic: conceptual
ms.assetid: f63bb62c-60da-40d5-ac14-4366608fe260
ms.openlocfilehash: 204ea9f86377eb8a5796f01cb81a9161163d9649
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65221886"
---
# <a name="value-types-modern-c"></a>值类型（现代 C++）

C++ 类是由默认值类型。 本主题提供介绍性概述的值类型和与其使用相关的问题。

## <a name="value-vs-reference-types"></a>值与引用类型

如前面所述，C++ 类是由默认值类型。 它们可以指定为引用类型，启用多态行为以支持面向对象的编程。 从内存和布局控件的角度来看有时查看值类型，而引用类型的多态的目的是有关基类和虚拟函数。 默认情况下，值类型是可复制，这意味着始终复制构造函数和复制赋值运算符。 对于引用类型，您使类不可复制 （禁用复制构造函数和复制赋值运算符），并使用支持其预期的多态性的虚拟析构函数。 值类型也是有关内容，这，它们是在复制时，始终让你可以单独修改的两个独立值。 有关标识的对象的类型是引用类型？ 出于此原因，"引用类型"也称为"多态类型"。

如果您真的想类似引用的类型 （基类、 虚函数），则需要显式禁用复制，如中所示`MyRefType`下面的代码中的类。

```cpp
// cl /EHsc /nologo /W4

class MyRefType {
private:
    MyRefType & operator=(const MyRefType &);
    MyRefType(const MyRefType &);
public:
    MyRefType () {}
};

int main()
{
    MyRefType Data1, Data2;
    // ...
    Data1 = Data2;
}
```

编译上述代码将导致以下错误：

```Output
test.cpp(15) : error C2248: 'MyRefType::operator =' : cannot access private member declared in class 'MyRefType'
        meow.cpp(5) : see declaration of 'MyRefType::operator ='
        meow.cpp(3) : see declaration of 'MyRefType'
```

## <a name="value-types-and-move-efficiency"></a>值类型和移动效率

由于新复制优化措施也避免了副本分配开销。 例如，字符串的字符串矢量中间插入时，将有任何复制的重新分配开销，仅移动-即使导致矢量本身的增长。 这也适用于其他操作，例如执行两个非常大的对象上的添加操作。 如何启用这些值操作优化？ 在某些 C++ 编译器，编译器将启用这为你隐式一样可以由编译器自动生成复制构造函数。 但是，在C++，您的类将需要为"选择"将通过在类定义中声明的分配和构造函数。 这可以通过使用双与号 (& &) 右值引用中的适当成员函数声明和定义移动构造函数和移动赋值方法。  此外需要插入正确的代码以"窃取开辟"，超出的源对象。

如何决定是否需要将移动启用了？ 如果您已经知道需要复制启用的构造，你可能希望将移动已启用，如果它可以是低于的深层副本。 但是，如果您知道需要移动的支持，它不一定表示你想启用复制。 这后一种情况下将名为"仅限移动的类型"。 已在标准库中的一个示例是`unique_ptr`。 注意，旧`auto_ptr`已弃用，并已被取代`unique_ptr`精确由于缺乏 C++ 早期版本中的移动语义支持。

通过使用移动语义中，你可以返回的值或插入的中部。 移动是副本的一种优化。 没有需要解决方法是堆分配。 请看下面的伪代码：

```cpp
#include <set>
#include <vector>
#include <string>
using namespace std;

//...
set<widget> LoadHugeData() {
    set<widget> ret;
    // ... load data from disk and populate ret
    return ret;
}
//...
widgets = LoadHugeData();   // efficient, no deep copy

vector<string> v = IfIHadAMillionStrings();
v.insert( begin(v)+v.size()/2, "scott" );   // efficient, no deep copy-shuffle
v.insert( begin(v)+v.size()/2, "Andrei" );  // (just 1M ptr/len assignments)
//...
HugeMatrix operator+(const HugeMatrix& , const HugeMatrix& );
HugeMatrix operator+(const HugeMatrix& ,       HugeMatrix&&);
HugeMatrix operator+(      HugeMatrix&&, const HugeMatrix& );
HugeMatrix operator+(      HugeMatrix&&,       HugeMatrix&&);
//...
hm5 = hm1+hm2+hm3+hm4+hm5;   // efficient, no extra copies
```

### <a name="enabling-move-for-appropriate-value-types"></a>启用适当的值类型的移动

对于移动可以是低于深层复制的值类似于类，启用移动构造和移动赋值为提高效率。 请看下面的伪代码：

```cpp
#include <memory>
#include <stdexcept>
using namespace std;
// ...
class my_class {
    unique_ptr<BigHugeData> data;
public:
    my_class( my_class&& other )   // move construction
        : data( move( other.data ) ) { }
    my_class& operator=( my_class&& other )   // move assignment
    { data = move( other.data ); return *this; }
    // ...
    void method() {   // check (if appropriate)
        if( !data )
            throw std::runtime_error("RUNTIME ERROR: Insufficient resources!");
    }
};
```

如果启用了复制构造/赋值，还启用移动构造/赋值，如果它可以是低于的深层副本。

某些*非值*类型是只移动的例如当无法克隆的资源，仅转移所有权。 示例：`unique_ptr`。

## <a name="section"></a>节

内容

## <a name="see-also"></a>请参阅

[C++ 类型系统（现代 C++）](../cpp/cpp-type-system-modern-cpp.md)<br/>
[欢迎回到 C++（现代 C++）](../cpp/welcome-back-to-cpp-modern-cpp.md)<br/>
[C++ 语言参考](../cpp/cpp-language-reference.md)<br/>
[C++ 标准库](../standard-library/cpp-standard-library-reference.md)
