---
title: 编译器错误 C3160
ms.date: 11/04/2016
f1_keywords:
- C3160
helpviewer_keywords:
- C3160
ms.assetid: a250c433-8adf-43b9-8dee-c3794e09b0a5
ms.openlocfilehash: 96fd97aa5021b7e1bc5226162f9c54ff4d6211b1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62175220"
---
# <a name="compiler-error-c3160"></a>编译器错误 C3160

“pointer”: 托管或 WinRT 类的数据成员不能具有此类型

内部垃圾回收指针可能会指向托管或 WinRT 类的内部。 因为它们比整个对象的指针慢，并且需要垃圾回收器进行特殊处理，因此你不能将内部托管的指针声明为类的成员。

以下示例生成 C3160：

```
// C3160.cpp
// compile with: /clr
ref struct A {
   // cannot create interior pointers inside a class
   interior_ptr<int> pg;   // C3160
   int g;   // OK
   int* pg2;   // OK
};

int main() {
   interior_ptr<int> pg2;   // OK
}
```
