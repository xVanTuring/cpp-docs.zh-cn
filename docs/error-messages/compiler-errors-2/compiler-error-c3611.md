---
title: 编译器错误 C3611
ms.date: 11/04/2016
f1_keywords:
- C3611
helpviewer_keywords:
- C3611
ms.assetid: 42f3e320-41de-420a-bd05-8924cab765aa
ms.openlocfilehash: 2d4c5cb02b1b8c5472502380fe7c74ff4a91954a
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "64345443"
---
# <a name="compiler-error-c3611"></a>编译器错误 C3611

function： 密封的函数不能具有纯说明符

密封的函数未正确声明。  有关详细信息，请参阅[密封](../../extensions/sealed-cpp-component-extensions.md)。

## <a name="example"></a>示例

下面的示例生成 C3611。

```
// C3611.cpp
// compile with: /clr /c

ref struct V {
   virtual void Test() sealed = 0;   // C3611
   virtual void Test2() sealed;   // OK
   virtual void Test3() = 0;   // OK
};
```