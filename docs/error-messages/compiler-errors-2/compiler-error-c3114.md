---
title: 编译器错误 C3114
ms.date: 11/04/2016
f1_keywords:
- C3114
helpviewer_keywords:
- C3114
ms.assetid: b5d2df4f-87d0-4292-9981-25c6a6013c05
ms.openlocfilehash: c5a4feae5c8805a27c020b532fd58e0562e46b6b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62404112"
---
# <a name="compiler-error-c3114"></a>编译器错误 C3114

参数： 不是有效的命名特性参数

为了使属性类数据成员是一个有效的命名参数，它不能标记`static`， `const`，或`literal`。 如果某个属性，该属性不能`static`并且必须具有 get 和 set 访问器。

有关详细信息，请参阅[属性](../../extensions/property-cpp-component-extensions.md)并[用户定义的特性](../../extensions/user-defined-attributes-cpp-component-extensions.md)。

## <a name="example"></a>示例

下面的示例生成 C3114。

```
// C3114.cpp
// compile with: /clr /c
public ref class A : System::Attribute {
public:
   static property int StaticProp {
      int get();
   }

   property int Prop2 {
      int get();
      void set(int i);
   }
};

[A(StaticProp=123)]   // C3114
public ref class R {};

[A(Prop2=123)]   // OK
public ref class S {};
```