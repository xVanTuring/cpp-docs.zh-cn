---
title: 编译器错误 C2448
ms.date: 11/04/2016
f1_keywords:
- C2448
helpviewer_keywords:
- C2448
ms.assetid: e255df3c-f861-4b4d-a193-8768cef061a5
ms.openlocfilehash: 915217ffbe848b2814e9960183854e09a80b9ee8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62230290"
---
# <a name="compiler-error-c2448"></a>编译器错误 C2448

identifier： 函数样式初始值设定项类似函数定义

函数定义不正确。

旧式 C 语言形式表可以导致此错误。

下面的示例生成 C2448:

```
// C2448.cpp
void func(c)
   int c;
{}   // C2448
```