---
title: 编译器错误 C3222
ms.date: 11/04/2016
f1_keywords:
- C3222
helpviewer_keywords:
- C3222
ms.assetid: 5624bde8-2fd0-4b8b-92ce-5dfbaf91cf93
ms.openlocfilehash: 9f2c245e98609c8da8f5f89902d5c51bbf9d2b4f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62364007"
---
# <a name="compiler-error-c3222"></a>编译器错误 C3222

“parameter”: 无法为托管或 WinRT 类型或泛型函数的成员函数声明默认自变量

不允许声明具有默认自变量的方法参数。 方法的重载形式是一种用于解决此问题的方式。 也就是说，定义具有相同名称但不带参数的方法，然后在方法体中初始化变量。

以下示例生成 C3222：

```
// C3222_2.cpp
// compile with: /clr
public ref class G {
   void f( int n = 0 );   // C3222
};
```
