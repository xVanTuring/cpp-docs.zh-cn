---
title: is_base_of 类
ms.date: 11/04/2016
f1_keywords:
- type_traits/std::is_base_of
helpviewer_keywords:
- is_base_of class
- is_base_of
ms.assetid: 436f6213-1d4c-4ffc-a588-fc7c4887dd86
ms.openlocfilehash: 345301b5eeed7b66f18a54e56b9bee6346078634
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383667"
---
# <a name="isbaseof-class"></a>is_base_of 类

测试一种类型是否是另一种类型的基类。

## <a name="syntax"></a>语法

```cpp
template <class Base, class Derived>
struct is_base_of;
```

### <a name="parameters"></a>参数

*基本*<br/>
要测试的基类。

*派生*<br/>
要测试的派生类型。

## <a name="remarks"></a>备注

如果类型谓词的实例将保留 true 类型*基*是类型的基类*派生*，否则为 false。

## <a name="example"></a>示例

```cpp
#include <type_traits>
#include <iostream>

struct base
    {
    int val;
    };

struct derived
    : public base
    {
    };

int main()
    {
    std::cout << "is_base_of<base, base> == " << std::boolalpha
        << std::is_base_of<base, base>::value << std::endl;
    std::cout << "is_base_of<base, derived> == " << std::boolalpha
        << std::is_base_of<base, derived>::value << std::endl;
    std::cout << "is_base_of<derived, base> == " << std::boolalpha
        << std::is_base_of<derived, base>::value << std::endl;

    return (0);
    }
```

```Output
is_base_of<base, base> == true
is_base_of<base, derived> == true
is_base_of<derived, base> == false
```

## <a name="requirements"></a>要求

**标头：**\<type_traits>

**命名空间：** std

## <a name="see-also"></a>请参阅

[<type_traits>](../standard-library/type-traits.md)<br/>
[is_convertible 类](../standard-library/is-convertible-class.md)<br/>
