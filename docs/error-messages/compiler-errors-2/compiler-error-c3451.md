---
title: 编译器错误 C3451
ms.date: 11/04/2016
f1_keywords:
- C3451
helpviewer_keywords:
- C3451
ms.assetid: a4897a69-e3e7-40bb-bb1c-598644904012
ms.openlocfilehash: 07cfda76af26ddb285be4f77131aaf48a20a761f
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65447852"
---
# <a name="compiler-error-c3451"></a>编译器错误 C3451

attribute： 不能将非托管的特性 type 应用

一个C++属性不能应用于 CLR 类型。 请参阅[C++的特性参考](../../windows/attributes/attributes-alphabetical-reference.md)有关详细信息。

有关详细信息，请参阅 [User-Defined Attributes](../../extensions/user-defined-attributes-cpp-component-extensions.md)。

为 Visual Studio 2005 执行的编译器一致性工作可以生成此错误： [uuid](../../windows/uuid-cpp-attributes.md)属性不再允许使用 CLR 编程对用户定义属性。 请改用 <xref:System.Runtime.InteropServices.GuidAttribute>。

## <a name="example"></a>示例

下面的示例生成 C3451。

```
// C3451.cpp
// compile with: /clr /c
using namespace System;
[ attribute(AttributeTargets::All) ]
public ref struct MyAttr {};

[ MyAttr, helpstring("test") ]   // C3451
// try the following line instead
// [ MyAttr ]
public ref struct ABC {};
```