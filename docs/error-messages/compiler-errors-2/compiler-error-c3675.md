---
title: 编译器错误 C3675
ms.date: 11/04/2016
f1_keywords:
- C3675
helpviewer_keywords:
- C3675
ms.assetid: 87461613-6633-430b-b95d-c7cb1bb63776
ms.openlocfilehash: e29e536bf89aef887dc043327e4b4596703d0538
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62363890"
---
# <a name="compiler-error-c3675"></a>编译器错误 C3675

function： 已保留，因为 property 被定义

声明一个简单的属性时，编译器将生成的 get 和 set 访问器方法和这些名称是存在于程序的范围。  通过预先计算 get_ 和 set_ 的属性名称形成编译器生成的名称。  因此，不能声明具有相同的名称的编译器生成的访问器函数。

有关更多信息，请参见 [property](../../extensions/property-cpp-component-extensions.md) 。

## <a name="example"></a>示例

下面的示例生成 C3675。

```
// C3675.cpp
// compile with: /clr /c
ref struct C {
public:
   property int Size;
   int get_Size() { return 0; }   // C3675
};
```