---
title: 编译器警告（等级 4）C4714
ms.date: 11/04/2016
f1_keywords:
- C4714
helpviewer_keywords:
- C4714
ms.assetid: 22c7fd0c-899d-4e9b-95f3-725b2c49fb46
ms.openlocfilehash: ed94e5b716a697ec96d7fecac75433823c9a67e9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62395178"
---
# <a name="compiler-warning-level-4-c4714"></a>编译器警告（等级 4）C4714

函数 function 标记为 __forceinline 未内联

为内联扩展选定了给定的函数，但编译器未执行内联。

尽管`__forceinline`是比编译器更强的指示`__inline`、 内联仍执行在编译器的判断力，但没有试探法用于确定该也会从内联此函数。

在某些情况下，编译器将不内联某个特定函数的机械的原因。 例如，编译器将不内联：

- 如果这会导致在混合使用这两种 SEH 的函数和C++EH。

- 某些函数使用复制构造上-GX EHs//eha 时按值传递的对象。

- -GX EHs//eha 上时按值返回一个不可展开对象的函数。

- 使用内联程序集没有-Og/Ox/O1/O2 进行编译时的函数。

- 使用变量参数列表的函数。

- 使用函数**尝试**(C++异常处理) 语句。

下面的示例生成 C4714:

```
// C4714.cpp
// compile with: /Ob1 /GX /W4
__forceinline void func1()
{
   try
   {
   }
   catch (...)
   {
   }
}

void func2()
{
   func1();   // C4714
}

int main()
{
}
```