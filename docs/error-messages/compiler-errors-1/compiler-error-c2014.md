---
title: 编译器错误 C2014
ms.date: 11/04/2016
f1_keywords:
- C2014
helpviewer_keywords:
- C2014
ms.assetid: 231d8e9c-48c0-4027-99a3-245d186275ec
ms.openlocfilehash: 58cf9867a9e36b304ab9da79084bc01dff453892
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62350697"
---
# <a name="compiler-error-c2014"></a>编译器错误 C2014

预处理器命令必须作为第一个非空白空间启动

`#`预处理器指令的符号必须是不是空白的行上的第一个字符。

下面的示例生成 C2014:

```
// C2014.cpp
int k; #include <stdio.h>   // C2014
```

可能的解决方法：

```
// C2014b.cpp
// compile with: /c
int k;
#include <stdio.h>
```