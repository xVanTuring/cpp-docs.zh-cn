---
title: 编译器警告（等级 1）C4659
ms.date: 11/04/2016
f1_keywords:
- C4659
helpviewer_keywords:
- C4659
ms.assetid: e29ba8db-7917-43f6-8e34-868b752279ae
ms.openlocfilehash: 2aef25e922d8f38ac7103b1b12ccb31c282f0403
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62374646"
---
# <a name="compiler-warning-level-1-c4659"></a>编译器警告（等级 1）C4659

\#杂注杂注： 行为未定义的保留段领域的使用，请使用 #pragma comment (linker，...)

.Drectve 选项用于将选项传递给链接器。 而是使用杂注[注释](../../preprocessor/comment-c-cpp.md)传递链接器选项。

```
// C4659.cpp
// compile with: /W1 /LD
#pragma code_seg(".drectve")   // C4659
```