---
title: 编译器错误 C2357
ms.date: 11/04/2016
f1_keywords:
- C2357
helpviewer_keywords:
- C2357
ms.assetid: d1083945-0ea2-4385-9e66-8c665978806c
ms.openlocfilehash: 1872672e776ad13bf16be5ae69729f4f68d8f3b0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62302028"
---
# <a name="compiler-error-c2357"></a>编译器错误 C2357

identifier： 必须是 type 类型的函数

你的代码声明版本`atexit`由编译器在内部声明的版本不匹配的函数。 声明`atexit`，如下所示：

```
int __cdecl atexit(void (__cdecl *)());
```

有关详细信息，请参阅[init_seg](../../preprocessor/init-seg.md)。

下面的示例生成 C2357:

```
// C2357.cpp
// compile with: /c
// C2357 expected
#pragma warning(disable : 4075)
// Uncomment the following line to resolve.
// int __cdecl myexit(void (__cdecl *)());
#pragma init_seg(".mine$m",myexit)
```