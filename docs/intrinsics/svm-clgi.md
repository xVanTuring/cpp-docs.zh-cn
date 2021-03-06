---
title: __svm_clgi
ms.date: 11/04/2016
f1_keywords:
- __svm_clgi
helpviewer_keywords:
- CLGI instruction
- __svm_clgi intrinsic
ms.assetid: 6640f5ab-9472-46f9-a042-e15c4f1ff858
ms.openlocfilehash: fe25141499a19a265e2ac3ec746664ecd6cc9a2e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62390303"
---
# <a name="svmclgi"></a>__svm_clgi

**Microsoft 专用**

清除全局中断标志。

## <a name="syntax"></a>语法

```
void __svm_clgi( void );
```

## <a name="remarks"></a>备注

`__svm_clgi` 函数等同于 `CLGI` 计算机指令。 全局中断标志确定微处理器忽略、 推迟，或处理的 I/O 完成、 硬件温度警报或调试异常等事件中断。

此函数支持主机的虚拟机监视器与来宾操作系统及其应用程序进行交互。 有关详细信息，搜索文档中，"AMD64 体系结构编程人员手动卷 2:系统编程，"文档数 24593，3.11，修订[AMD corporation](https://developer.amd.com/resources/developer-guides-manuals/)站点。

## <a name="requirements"></a>要求

|内部函数|体系结构|
|---------------|------------------|
|`__svm_clgi`|x86、x64|

**标头文件** \<intrin.h >

**结束 Microsoft 专用**

## <a name="see-also"></a>请参阅

[编译器内部函数](../intrinsics/compiler-intrinsics.md)<br/>
[__svm_stgi](../intrinsics/svm-stgi.md)