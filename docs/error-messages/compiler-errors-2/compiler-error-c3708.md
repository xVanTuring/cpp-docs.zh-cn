---
title: 编译器错误 C3708
ms.date: 11/04/2016
f1_keywords:
- C3708
helpviewer_keywords:
- C3708
ms.assetid: 45e71564-9c7f-437f-98d8-a735ce162ed0
ms.openlocfilehash: 7ee9d59f12cc9e748b08b3e4a704420ea5c58be6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62328505"
---
# <a name="compiler-error-c3708"></a>编译器错误 C3708

interface: keyword; 使用不当必须是兼容事件源的成员

若要声明为事件的接口，事件声明必须是事件源。

下面的示例生成 C3708:

```
// C3708.cpp
// compile with: /c
#define _ATL_ATTRIBUTES 1
#include "atlbase.h"
#include "atlcom.h"

[ module(name="MyLibrary")];

[ object, uuid("00000000-0000-0000-0000-000000000001") ]
__interface I {
   HRESULT func();
};

[ object, uuid("00000000-0000-0000-0000-000000000002") ]
__interface II {
   HRESULT func();
};

__event __interface I;   // C3708

// put the event in an event source
[ coclass, event_source(com), uuid("00000000-0000-0000-0000-000000000003") ]
struct E : II {
   __event __interface II;
};
```