---
title: high_property_prefixes
ms.date: 10/18/2018
f1_keywords:
- high_property_prefixes
helpviewer_keywords:
- high_property_prefixes attribute
ms.assetid: 91c6cc2b-19b6-4aba-8831-d9e5cccb58b5
ms.openlocfilehash: 3f8975ec9737e02bb1216166cc6c241549e95a07
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62409832"
---
# <a name="highpropertyprefixes"></a>high_property_prefixes

**C++特定**

指定用于三个属性方法的备用前缀。

## <a name="syntax"></a>语法

```
high_property_prefixes("GetPrefix","PutPrefix","PutRefPrefix")
```

### <a name="parameters"></a>参数

*GetPrefix*<br/>
前缀用于`propget`方法。

*PutPrefix*<br/>
前缀用于`propput`方法。

*PutRefPrefix*<br/>
前缀用于`propputref`方法。

## <a name="remarks"></a>备注

默认情况下，高级错误处理`propget`， `propput`，并`propputref`使用的前缀命名的成员函数公开方法`Get`， `Put`，和`PutRef`分别。

**结束C++特定**

## <a name="see-also"></a>请参阅

[#import 属性](../preprocessor/hash-import-attributes-cpp.md)<br/>
[#import 指令](../preprocessor/hash-import-directive-cpp.md)