---
title: 编译器错误 C2511
ms.date: 11/04/2016
f1_keywords:
- C2511
helpviewer_keywords:
- C2511
ms.assetid: df999efe-fe2b-418b-bb55-4af6a0592631
ms.openlocfilehash: 9d9ba48b0607e7a30b8748d4e9ae4f7025f11dea
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62165016"
---
# <a name="compiler-error-c2511"></a>编译器错误 C2511

identifier： 重载的 class 中找不到成员函数

任何版本的函数使用指定的参数不声明。  可能的原因：

1. 错误的参数传递给函数。

1. 在错误的顺序传递参数。

1. 参数名称拼写不正确。

下面的示例生成 C2511:

```
// C2511.cpp
// compile with: /c
class C {
   int c_2;
   int Func(char *, char *);
};

int C::Func(char *, char *, int i) {   // C2511
// try the following line instead
// int C::Func(char *, char *) {
   return 0;
}
```