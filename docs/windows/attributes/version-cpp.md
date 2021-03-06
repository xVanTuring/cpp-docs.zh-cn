---
title: 版本 (C++ COM 属性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.version
helpviewer_keywords:
- version attribute
- version information, version attribute
ms.assetid: db6ce5d8-82c2-4329-b1a8-8ca2f67342cb
ms.openlocfilehash: fe1df9e12b9adbf9ce55978fd3479f7e740ddc96
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62407154"
---
# <a name="version-c"></a>version (C++)

标识类的多个版本间的特定版本。

## <a name="syntax"></a>语法

```cpp
[ version("version") ]
```

### <a name="parameters"></a>参数

*版本*<br/>
版本号`coclass`。 如果未指定，则将在.idl 文件中放置 1.0。

## <a name="remarks"></a>备注

**版本**C++属性具有相同的功能[版本](/windows/desktop/Midl/version)MIDL 特性并将传递给生成的.idl 文件。

## <a name="example"></a>示例

请参阅[可绑定](bindable.md)的示例使用的示例**版本**。

## <a name="requirements"></a>要求

### <a name="attribute-context"></a>特性上下文

|||
|-|-|
|**适用对象**|**类**，**结构**|
|**可重复**|否|
|**必需的特性**|**coclass**|
|**无效的特性**|None|

有关特性上下文的详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>请参阅

[编译器特性](compiler-attributes.md)<br/>
[类特性](class-attributes.md)