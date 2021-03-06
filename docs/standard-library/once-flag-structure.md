---
title: once_flag 结构
ms.date: 09/17/2018
f1_keywords:
- mutex/std::once_flag
ms.assetid: 71bfb88d-ca8c-4082-a6e1-ff52151e8629
ms.openlocfilehash: 004a5545e2eccab83b0846e2ae30b88c8431c99d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62371433"
---
# <a name="onceflag-structure"></a>once_flag 结构

表示**struct**模板函数一起使用[call_once](../standard-library/mutex-functions.md#call_once)以确保初始化代码调用一次，即使出现多个执行线程。

## <a name="syntax"></a>语法

struct once_flag { constexpr once_flag() noexcept; };

## <a name="remarks"></a>备注

`once_flag` **结构**只有一个默认构造函数。

可以创建 `once_flag` 类型的对象，但不能复制它们。

## <a name="requirements"></a>要求

**标头：** \<互斥体 >

**命名空间：** std

## <a name="see-also"></a>请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)<br/>
[\<mutex>](../standard-library/mutex.md)<br/>
