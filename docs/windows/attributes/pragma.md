---
title: 杂注 (C++ COM 属性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.pragma
helpviewer_keywords:
- pragma attribute
ms.assetid: 3f90d023-b8b5-4007-8311-008bb72cbea1
ms.openlocfilehash: 159e1570c2bde07bb4df8fa904a519e8e0018a6a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62407453"
---
# <a name="pragma"></a>pragma

将指定的字符串发出到生成的.idl 文件而不使用引号引起来。

## <a name="syntax"></a>语法

```cpp
[ pragma(pragma_statement) ];
```

### <a name="parameters"></a>参数

*pragma_statement*<br/>
你想要转到生成的.idl 文件杂注。

## <a name="remarks"></a>备注

**杂注**C++属性具有相同的功能[杂注](/windows/desktop/Midl/pragma)MIDL 特性。

## <a name="example"></a>示例

```cpp
// cpp_attr_ref_pragma.cpp
// compile with: /LD
#include "unknwn.h"
[module(name="MyLib")];
[pragma(pack(4))];

[dispinterface, uuid("00000000-0000-0000-0000-000000000001")]
__interface A
{
   [id(1)] HRESULT MyMethod ([in, satype("BSTR")] SAFEARRAY **p);
};
```

## <a name="requirements"></a>要求

### <a name="attribute-context"></a>特性上下文

|||
|-|-|
|**适用对象**|任何位置|
|**可重复**|否|
|**必需的特性**|None|
|**无效的特性**|None|

有关特性上下文的详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>请参阅

[IDL 特性](idl-attributes.md)<br/>
[独立特性](stand-alone-attributes.md)<br/>
[pack](../../preprocessor/pack.md)