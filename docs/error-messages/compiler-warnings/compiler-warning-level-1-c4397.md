---
title: 编译器警告（等级 1）C4397
ms.date: 11/04/2016
f1_keywords:
- C4397
helpviewer_keywords:
- C4397
ms.assetid: 6346fdc2-dbbf-4fba-803a-32b0d0a707be
ms.openlocfilehash: 7f0a3c31f460a66523ed1c327cee097dc890bbeb
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65447670"
---
# <a name="compiler-warning-level-1-c4397"></a>编译器警告（等级 1）C4397

已忽略 DefaultCharSetAttribute

<xref:System.Runtime.InteropServices.DefaultCharSetAttribute> Microsoft 将忽略C++编译器。 若要指定为 DLL 设置的字符，使用 DllImport 的 CharSet 选项。 有关详细信息，请参阅[使用C++互操作 (隐式 PInvoke)](../../dotnet/using-cpp-interop-implicit-pinvoke.md)。

## <a name="example"></a>示例

下面的示例生成 C4397。

```
// C4397.cpp
// compile with: /W1 /c /clr
using namespace System;
using namespace System::Runtime::InteropServices;

[module:DefaultCharSetAttribute(CharSet::Unicode)];   // C4397

[DllImport("kernel32", EntryPoint="CloseHandle", CharSet=CharSet::Unicode)]   // OK
extern "C" bool ImportDefault(IntPtr hObject);

public ref class MySettingVC {
public:
   void method() {
      ImportDefault(IntPtr::Zero);
   }
};

[StructLayout(LayoutKind::Explicit)]
public ref struct StructDefault1{};

public ref class ClassDefault1{};
```