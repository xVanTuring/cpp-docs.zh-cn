---
title: 析构函数 (C++)
ms.date: 05/06/2019
helpviewer_keywords:
- objects [C++], destroying
- destructors, C++
ms.assetid: afa859b0-f3bc-4c4d-b250-c68b335b6004
ms.openlocfilehash: 7bcfbd1ca95d98421fd2d58b595dd3309cdf8011
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65222449"
---
# <a name="destructors-c"></a>析构函数 (C++)

析构函数是超出范围或通过调用显式销毁的对象时，会自动调用的成员函数**删除**。 析构函数有同名的类，前面是波形符 (`~`)。 例如，声明 `String` 类的析构函数：`~String()`。

如果未定义析构函数，编译器将提供默认值对于许多类，这已足够。 只需定义自定义的析构函数时，类存储需要释放的系统资源的句柄或拥有内存的指针指向的目标。

请考虑 `String` 类的以下声明：

```cpp
// spec1_destructors.cpp
#include <string>

class String {
public:
   String( char *ch );  // Declare constructor
   ~String();           //  and destructor.
private:
   char    *_text;
   size_t  sizeOfText;
};

// Define the constructor.
String::String( char *ch ) {
   sizeOfText = strlen( ch ) + 1;

   // Dynamically allocate the correct amount of memory.
   _text = new char[ sizeOfText ];

   // If the allocation succeeds, copy the initialization string.
   if( _text )
      strcpy_s( _text, sizeOfText, ch );
}

// Define the destructor.
String::~String() {
   // Deallocate the memory that was previously reserved
   //  for this string.
   delete[] _text;
}

int main() {
   String str("The piper in the glen...");
}
```

在前面的示例中，析构函数`String::~String`使用**删除**运算符先解除分配，文本存储为动态分配的空间。

## <a name="declaring-destructors"></a>声明析构函数

析构函数是具有与类相同的名称但前面是波形符 (`~`) 的函数

多个规则管理析构函数的声明。 析构函数：

- 不接受自变量。

- 不返回值 (或**void**)。

- 不能声明为**const**，**易失性**，或**静态**。 但是，它们可以调用对于对象的析构声明为**const**，**易失性**，或**静态**。

- 可以声明为**虚拟**。 通过使用虚拟析构函数，无需知道对象的类型即可销毁对象 - 使用虚函数机制调用该对象的正确析构函数。 请注意，析构函数也可以声明为抽象类的纯虚函数。

## <a name="using-destructors"></a>使用构造函数

当下列事件之一发生时，将调用析构函数：

- 具有块范围的本地（自动）对象超出范围。

- 使用分配的对象**新**运算符显式解除分配使用**删除**。

- 临时对象的生存期结束。

- 程序结束，并且存在全局或静态对象。

- 使用析构函数的完全限定名显式调用了析构函数。

析构函数可以随意调用类成员函数和访问类成员数据。

有两个的限制的析构函数：

- 不能采用其地址。

- 派生的类不会继承其基类的析构函数。

## <a name="order-of-destruction"></a>析构的顺序

当对象超出范围或被删除时，其完整析构中的事件序列如下所示：

1. 将调用该类的析构函数，并且会执行该析构函数的主体。

1. 按照非静态成员对象的析构函数在类声明中的显示顺序的相反顺序调用这些函数。 这些成员的构造中使用的可选成员优化列表不会影响构造或析构的顺序。

1. 声明的相反顺序调用非虚拟基类的析构函数。

1. 虚拟基类的析构函数以声明的相反顺序被调用。

```cpp
// order_of_destruction.cpp
#include <cstdio>

struct A1      { virtual ~A1() { printf("A1 dtor\n"); } };
struct A2 : A1 { virtual ~A2() { printf("A2 dtor\n"); } };
struct A3 : A2 { virtual ~A3() { printf("A3 dtor\n"); } };

struct B1      { ~B1() { printf("B1 dtor\n"); } };
struct B2 : B1 { ~B2() { printf("B2 dtor\n"); } };
struct B3 : B2 { ~B3() { printf("B3 dtor\n"); } };

int main() {
   A1 * a = new A3;
   delete a;
   printf("\n");

   B1 * b = new B3;
   delete b;
   printf("\n");

   B3 * b2 = new B3;
   delete b2;
}

Output: A3 dtor
A2 dtor
A1 dtor

B1 dtor

B3 dtor
B2 dtor
B1 dtor
```

### <a name="virtual-base-classes"></a>虚拟基类

按照与虚拟基类在定向非循环图形中显示的顺序的相反顺序调用这些虚拟基类的析构函数（深度优先、从左到右、后序遍历）。 下图描述了继承关系图。

![显示虚拟基类的继承关系图](../cpp/media/vc392j1.gif "显示虚拟基类的继承关系图") <br/>
显示虚拟基类的继承图

下面列出了图中显示的类的类头。

```cpp
class A
class B
class C : virtual public A, virtual public B
class D : virtual public A, virtual public B
class E : public C, public D, virtual public B
```

为了确定 `E` 类型的对象的虚拟基类的析构顺序，编译器将通过应用以下算法来生成列表：

1. 向左遍历关系图，并从关系图中的最深点开始（在此示例中，为 `E`）。

1. 执行左移遍历，直到访问了所有节点。 记下当前节点的名称。

1. 重新访问上一个节点（向下并向右）以查明要记住的节点是否为虚拟基类。

1. 如果记住的节点是虚拟基类，请浏览列表以查看是否已将其输入。 如果它不是虚拟基类，则将其忽略。

1. 如果记住的节点尚未包含在列表中，请将其添加到列表的底部。

1. 向上遍历关系图并沿下一个路径向右遍历。

1. 转到步骤 2。

1. 在用完最后一个向上路径时，请记下当前节点的名称。

1. 转到步骤 3。

1. 继续执行此过程，直到底部节点再次成为当前节点。

因此，对于 `E` 类，析构顺序为：

1. 非虚拟基类`E`。

1. 非虚拟基类`D`。

1. 非虚拟基类`C`。

1. 虚拟基类 `B`。

1. 虚拟基类 `A`。

此过程将生成唯一项的有序列表。 任何类名均不会出现两次。 在构造列表后，将以相反的顺序遍历该列表，并且将调用列表中每个类（从最后一个到第一个）的析构函数。

如果某个类中的构造函数或析构函数依赖于要先创建或保留更长时间的另一个组件（例如，如果 `A` 的析构函数（上图中所示）依赖于执行其代码时仍存在 `B`），则构造或析构的顺序特别重要，反之亦然。

继承关系图中各个类之间的这种相互依赖项本质上是危险的，因为稍后派生类可以更改最左边的路径，从而更改构造和析构的顺序。

### <a name="non-virtual-base-classes"></a>非虚拟基类

声明基类名称的相反顺序调用非虚拟基类的析构函数。 考虑下列类声明：

```cpp
class MultInherit : public Base1, public Base2
...
```

在前面的示例中，先于 `Base2` 的析构函数调用 `Base1` 的析构函数。

## <a name="explicit-destructor-calls"></a>显式析构函数调用

很少需要显式调用析构函数。 但是，对置于绝对地址的对象进行清理会很有用。 通常使用用户定义分配这些对象**新**采用位置自变量的运算符。 **删除**运算符不能释放该内存，因为它不从自由存储分配 (有关详细信息，请参阅[新和 delete 运算符](../cpp/new-and-delete-operators.md))。 但是，对析构函数的调用可以执行相应的清理。 若要显式调用 `s` 类的对象 `String` 的析构函数，请使用下列语句之一：

```cpp
s.String::~String();     // non-virtual call
ps->String::~String();   // non-virtual call

s.~String();       // Virtual call
ps->~String();     // Virtual call
```

可以使用对前面显示的析构函数的显式调用的表示法，无论类型是否定义了析构函数。 这允许您进行此类显式调用，而无需了解是否为此类型定义了析构函数。 显式调用析构函数，其中未定义的析构函数无效。