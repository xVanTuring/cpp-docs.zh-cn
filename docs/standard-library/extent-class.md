---
title: extent 类
ms.date: 11/04/2016
f1_keywords:
- type_traits/std::extent
helpviewer_keywords:
- extent class
- extent
ms.assetid: 6d16263d-90b2-4330-9ec7-b59ed898792d
ms.openlocfilehash: 7463b424d15ee86f851b7d81953abf3fe1c98fee
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62393969"
---
# <a name="extent-class"></a>extent 类

获取数组维度。

## <a name="syntax"></a>语法

```cpp
template <class Ty, unsigned I = 0>
struct extent;
```

### <a name="parameters"></a>参数

*Ty*<br/>
要查询的类型。

*I*<br/>
绑定到查询的数组。

## <a name="remarks"></a>备注

如果*Ty*是至少具有一个数组类型*我*维度，则类型查询保留的元素数中由指定的维度*我*。如果*Ty*不是数组类型或它的级别小于*我*，或者，如果*我*为零并*Ty*属于类型"未知绑定的数组的`U`"，则类型查询保留值 0。

## <a name="example"></a>示例

```cpp
// std__type_traits__extent.cpp
// compile with: /EHsc
#include <type_traits>
#include <iostream>

int main()
    {
    std::cout << "extent 0 == "
        << std::extent<int[5][10]>::value << std::endl;
    std::cout << "extent 1 == "
        << std::extent<int[5][10], 1>::value << std::endl;

    return (0);
    }
```

```Output
extent 0 == 5
extent 1 == 10
```

## <a name="requirements"></a>要求

**标头：**\<type_traits>

**命名空间：** std

## <a name="see-also"></a>请参阅

[<type_traits>](../standard-library/type-traits.md)<br/>
[remove_all_extents 类](../standard-library/remove-all-extents-class.md)<br/>
[remove_extent 类](../standard-library/remove-extent-class.md)<br/>
