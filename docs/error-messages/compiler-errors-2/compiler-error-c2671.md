---
title: 编译器错误 C2671
ms.date: 11/04/2016
f1_keywords:
- C2671
helpviewer_keywords:
- C2671
ms.assetid: fc0ee40f-c8f3-408f-b89d-745d149c4169
ms.openlocfilehash: 92ed646b0e4c5d2bbc6556c2a7b1ef66d8192ec1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62165068"
---
# <a name="compiler-error-c2671"></a>编译器错误 C2671

function： 静态成员函数没有 this 指针

一个`static`成员函数尝试访问`this`。

下面的示例生成 C2671:

```
// C2671.cpp
struct S {
   static S* const func() { return this; }  // C2671
};
```