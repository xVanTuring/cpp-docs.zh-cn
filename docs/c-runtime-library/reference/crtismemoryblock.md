---
title: _CrtIsMemoryBlock
ms.date: 11/04/2016
apiname:
- _CrtIsMemoryBlock
apilocation:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
apitype: DLLExport
f1_keywords:
- CrtlsMemoryBlock
- _CrtIsMemoryBlock
helpviewer_keywords:
- _CrtIsMemoryBlock function
- CrtIsMemoryBlock function
ms.assetid: f7cbbc60-3690-4da0-a07b-68fd7f250273
ms.openlocfilehash: c4a85ebeb45552c6f5355853de2a45766d6bc984
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62339892"
---
# <a name="crtismemoryblock"></a>_CrtIsMemoryBlock

确认指定的内存块位于本地堆，并且具有有效的调试堆块类型标识符（仅限调试版本）。

## <a name="syntax"></a>语法

```C
int _CrtIsMemoryBlock(
   const void *userData,
   unsigned int size,
   long *requestNumber,
   char **filename,
   int *linenumber
);
```

### <a name="parameters"></a>参数

*userData*<br/>
指向要验证的内存块开头的指针。

*size*<br/>
指定块的大小（以字节为单位）。

*requestNumber*<br/>
指向块分配编号或**NULL**。

*filename*<br/>
指向已请求块的源文件名或**NULL**。

*linenumber*<br/>
指向源文件中的行号或**NULL**。

## <a name="return-value"></a>返回值

**_CrtIsMemoryBlock**将返回**TRUE**如果指定的内存块位于本地堆，并且具有有效的调试堆块类型标识符; 否则，该函数返回**FALSE**。

## <a name="remarks"></a>备注

**_CrtIsMemoryBlock**函数将验证指定的内存块位于应用程序的本地堆，并且它具有有效的块类型标识符。 此函数还可用于获取最初请求内存块分配的对象分配序号和源文件名/行号。 传递非**NULL**值为*requestNumber*， *filename*，或者*linenumber*参数的原因 **_CrtIsMemoryBlock**将这些参数设置为内存块调试标头中的值，如果它找到块位于本地堆。 当[_DEBUG](../../c-runtime-library/debug.md)未定义，则调用 **_CrtIsMemoryBlock**在预处理过程中删除。

如果 **_CrtIsMemoryBlock**失败，则返回**FALSE**和输出参数将初始化为默认值： *requestNumber*和**lineNumber**设置为 0 和*文件名*设置为**NULL**。

因为此函数返回 **TRUE** 或 **FALSE**，因此可将它传递到其中一个 [_ASSERT](assert-asserte-assert-expr-macros.md) 宏，以创建一种简单的调试错误处理机制。 如果本地堆中没有指定的地址，则以下示例将导致断言失败：

```C
_ASSERTE( _CrtIsMemoryBlock( userData, size, &requestNumber,
          &filename, &linenumber ) );
```

详细了解如何 **_CrtIsMemoryBlock**可以与其他调试函数和宏一起使用，请参阅[用于报告的宏](/visualstudio/debugger/macros-for-reporting)。 有关如何在基堆的调试版本中分配、初始化和管理内存块的信息，请参阅 [CRT Debug Heap Details](/visualstudio/debugger/crt-debug-heap-details)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_CrtIsMemoryBlock**|\<crtdbg.h>|

有关更多兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>库

仅限 [C 运行时库](../../c-runtime-library/crt-library-features.md)的调试版本。

## <a name="example"></a>示例

请参阅 [_CrtIsValidHeapPointer](crtisvalidheappointer.md) 主题的示例。

## <a name="see-also"></a>请参阅

[调试例程](../../c-runtime-library/debug-routines.md)<br/>
