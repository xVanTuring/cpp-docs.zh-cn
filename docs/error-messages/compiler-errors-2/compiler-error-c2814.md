---
title: 编译器错误 C2814
ms.date: 11/04/2016
f1_keywords:
- C2814
helpviewer_keywords:
- C2814
ms.assetid: 7d165136-a08b-4497-a76d-60a21bb19404
ms.openlocfilehash: 6562e8a0968f83a0e7e968b538b4d94dc1047fa5
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62329551"
---
# <a name="compiler-error-c2814"></a>编译器错误 C2814

“member”：本机类型不能嵌套在托管类型或 WinRT 类型“type”内

## <a name="example"></a>示例

本机类型不能嵌套在 CLR 或 WinRT 类型中。 下面的示例生成 C2814，并演示如何修复此错误。

```
// C2814.cpp
// compile with: /clr /c
ref class A {
   class B {};   // C2814
   ref class C {};   // OK
};
```
