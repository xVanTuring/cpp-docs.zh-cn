---
title: __svm_vmsave
ms.date: 11/04/2016
f1_keywords:
- __svm_vmsave
helpviewer_keywords:
- VMSAVE instruction
- __svm_vmsave intrinsic
ms.assetid: 617a60bd-8514-4ba1-8066-bcf4dd481030
ms.openlocfilehash: d683a13f636db9683b4a7c8d075ad6c3c88c2aed
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62390186"
---
# <a name="svmvmsave"></a>__svm_vmsave

**Microsoft 专用**

在指定的虚拟机控制块 (VMCB) 中存储处理器状态的子集。

## <a name="syntax"></a>语法

```
void __svm_vmsave(
   size_t VmcbPhysicalAddress
);
```

#### <a name="parameters"></a>参数

|参数|描述|
|---------------|-----------------|
|*VmcbPhysicalAddress*|[in]VMCB 物理地址。|

## <a name="remarks"></a>备注

`__svm_vmsave` 函数等同于 `VMSAVE` 计算机指令。 此函数支持主机的虚拟机监视器与来宾操作系统及其应用程序进行交互。 有关详细信息，搜索文档中，"AMD64 体系结构编程人员手动卷 2:系统编程，"文档数 24593，3.11 或更高版本，在修订[AMD Corporation](https://developer.amd.com/resources/developer-guides-manuals/)站点。

## <a name="requirements"></a>要求

|内部函数|体系结构|
|---------------|------------------|
|`__svm_vmsave`|x86、x64|

**标头文件** \<intrin.h >

**结束 Microsoft 专用**

## <a name="see-also"></a>请参阅

[编译器内部函数](../intrinsics/compiler-intrinsics.md)<br/>
[__svm_vmrun](../intrinsics/svm-vmrun.md)<br/>
[__svm_vmload](../intrinsics/svm-vmload.md)