---
title: 编译器警告 （等级 3） C4073
ms.date: 11/04/2016
f1_keywords:
- C4073
helpviewer_keywords:
- C4073
ms.assetid: 50081a6e-6acd-45ff-8484-9b1ea926cc5c
ms.openlocfilehash: db39f76f9bfdd46c300ea6e3738a63b636fe0a03
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62402328"
---
# <a name="compiler-warning-level-3-c4073"></a>编译器警告 （等级 3） C4073

初始值设定项放置在库初始化区域中

只有第三方库开发人员应使用库初始化区域中，通过指定[#pragma init_seg](../../preprocessor/init-seg.md)。 下面的示例生成 C4073:

```
// C4073.cpp
// compile with: /W3
#pragma init_seg(lib)   // C4073

// try this line to resolve the warning
// #pragma init_seg(user)

int main() {
}
```