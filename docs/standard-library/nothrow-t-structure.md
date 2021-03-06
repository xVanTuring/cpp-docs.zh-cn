---
title: nothrow_t 结构
ms.date: 11/04/2016
f1_keywords:
- nothrow_t
helpviewer_keywords:
- nothrow_t class
ms.assetid: dc7d5d42-ed5a-4919-88fe-bbad519b7a1d
ms.openlocfilehash: 2313c436a1fd25149fa7ea72f122a6f323b40028
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62223618"
---
# <a name="nothrowt-structure"></a>nothrow_t 结构

该结构用作运算符 new 的函数参数，指示函数应返回一个 null 指针来报告分配失败，而不是引发异常。

## <a name="syntax"></a>语法

```cpp
struct std::nothrow_t {};
```

## <a name="remarks"></a>备注

该结构可帮助编译器选择正确版本的构造函数。 [nothrow](../standard-library/new-functions.md#nothrow) 是 `std::nothrow_t` 类型的对象的同义词。

## <a name="example"></a>示例

有关如何将 `std::nothrow_t` 用作函数参数的示例，请参阅[运算符 new](../standard-library/new-operators.md#op_new) 和[运算符 new&#91;&#93;](../standard-library/new-operators.md#op_new_arr)。

## <a name="requirements"></a>要求

**标头：**\<new>

**命名空间：** std

## <a name="see-also"></a>请参阅

[C++ 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)<br/>
