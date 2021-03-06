---
title: uuid（C++ 特性）
ms.date: 10/02/2018
f1_keywords:
- vc-attr.uuid
helpviewer_keywords:
- uuid attribute
ms.assetid: 90562a94-5e28-451b-a4b0-cadda7f66efe
ms.openlocfilehash: eae79f9a4d0af6375834c0792c4004f52a16e07e
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65448929"
---
# <a name="uuid-c-attributes"></a>uuid（C++ 特性）

指定类或接口的唯一 ID。

## <a name="syntax"></a>语法

```cpp
[ uuid(
   "uuid"
) ]
```

### <a name="parameters"></a>参数

*uuid*<br/>
一个 128 位的唯一标识符。

## <a name="remarks"></a>备注

如果未指定的接口或类定义**uuid** C++属性，则 MicrosoftC++编译器将提供一个。 当指定**uuid**，必须包括引号。

如果未指定**uuid**，则编译器将在一台计算机上的不同的属性项目中生成的接口或类具有相同的名称相同的 GUID。

您可以使用 Uuidgen.exe 或 Guidgen.exe 生成你自己的唯一 Id。 (若要运行这些工具，请单击**启动**然后单击**运行**菜单上。 然后输入所需的工具的名称。）

也不使用 ATL 的项目中使用时，指定**uuid**属性是与指定[uuid](../../cpp/uuid-cpp.md) **__declspec**修饰符。 若要检索**uuid**类，可以使用[__uuidof](../../cpp/uuidof-operator.md)

## <a name="example"></a>示例

请参阅[可绑定](bindable.md)的示例使用的示例**uuid**。

## <a name="requirements"></a>要求

### <a name="attribute-context"></a>特性上下文

|||
|-|-|
|**适用对象**|**类**， **struct**，**接口**，**联合**，**枚举**|
|**可重复**|否|
|**必需的特性**|None|
|**无效的特性**|None|

有关特性上下文的详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>请参阅

[IDL 特性](idl-attributes.md)<br/>
[接口特性](interface-attributes.md)<br/>
[类特性](class-attributes.md)<br/>
[Typedef、Enum、Union 和 Struct 特性](typedef-enum-union-and-struct-attributes.md)<br/>
[uuid](/windows/desktop/Midl/uuid)