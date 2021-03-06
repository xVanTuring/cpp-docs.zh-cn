---
title: 编译器警告（等级 4）C4239
ms.date: 11/04/2016
f1_keywords:
- C4239
helpviewer_keywords:
- C4239
ms.assetid: a23dc16a-649e-4870-9a24-275de1584fcd
ms.openlocfilehash: 067d1aef41280f4d14fe799e4f4ee26a9f1b9f5a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62401015"
---
# <a name="compiler-warning-level-4-c4239"></a>编译器警告（等级 4）C4239

使用了非标准扩展: token： 从 type 到 type 的转换

此类型转换不允许通过C++允许标准，但它作为扩展。 此警告是始终后跟至少一个行的说明，以描述所违反的语言规则。

## <a name="example"></a>示例

下面的示例生成 C4239。

```
// C4239.cpp
// compile with: /W4 /c
struct C {
   C() {}
};

void func(void) {
   C & rC = C();   // C4239
   const C & rC2 = C();   // OK
   rC2;
}
```

## <a name="example"></a>示例

严格不允许从整型类型转换为枚举类型。

下面的示例生成 C4239。

```
// C4239b.cpp
// compile with: /W4 /c
enum E { value };
struct S {
   E e : 2;
} s = { 5 };   // C4239
// try the following line instead
// } s = { (E)5 };
```