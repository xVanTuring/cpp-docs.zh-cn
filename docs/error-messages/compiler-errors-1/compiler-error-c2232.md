---
title: 编译器错误 C2232
ms.date: 11/04/2016
f1_keywords:
- C2232
helpviewer_keywords:
- C2232
ms.assetid: 76f302b7-30a7-4a81-9a39-b4edde33b54c
ms.openlocfilehash: f1478c2d06ab535a532b1be45c2db69050afe7b4
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62376635"
---
# <a name="compiler-error-c2232"></a>编译器错误 C2232

->： 左的操作数具有类键类型，使用。

`->` 运算符左侧的操作数不是指针。 对于类、 结构或联合使用句点 （.） 运算符。

下面的示例生成 C2232：

```
// C2232.c
struct X {
    int member;
} x, *px;
int main() {
    x->member = 0;   // C2232, x is not a pointer

    px->member = 0;
    x.member = 0;
}
```