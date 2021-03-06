---
title: fputs、fputws
ms.date: 11/04/2016
apiname:
- fputs
- fputws
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
- api-ms-win-crt-stdio-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- fputs
- fputws
- _fputts
helpviewer_keywords:
- streams, writing strings to
- fputws function
- _fputts function
- fputs function
- fputts function
ms.assetid: d48c82b8-aa17-4830-8c7d-30442ddbb326
ms.openlocfilehash: 3f7c7cff3300ae28717062a41aebd9e19c0cb5e0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62287962"
---
# <a name="fputs-fputws"></a>fputs、fputws

将字符串写入流。

## <a name="syntax"></a>语法

```C
int fputs(
   const char *str,
   FILE *stream
);
int fputws(
   const wchar_t *str,
   FILE *stream
);
```

### <a name="parameters"></a>参数

*str*<br/>
输出字符串。

*stream*<br/>
指向**文件**结构的指针。

## <a name="return-value"></a>返回值

如果成功，其中每个函数都将返回一个非负值。 发生错误时， **fputs**并**fputws**返回**EOF**。 如果*str*或*流*是 null 指针，这些函数将调用无效参数处理程序，如中所述[参数验证](../../c-runtime-library/parameter-validation.md)。 如果允许继续执行，这些函数将设置**errno**到**EINVAL** ，然后**fputs**返回**EOF**，和**fputws**将返回**WEOF**。

有关这些代码以及其他错误代码的详细信息，请参阅 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>备注

每个函数将副本*str*到输出*流*当前位置。 **fputws**将复制的宽字符自变量*str*到*流*作为多字节字符字符串或宽字符字符串根据*流*分别在文本模式还是二进制模式中打开。 函数不会复制终止的 null 字符。

如果在 ANSI 模式下打开流，则这两个函数行为相同。 **fputs**目前不支持输出到 UNICODE 流。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_fputts**|**fputs**|**fputs**|**fputws**|

## <a name="requirements"></a>要求

|函数|必需的标头|
|--------------|---------------------|
|**fputs**|\<stdio.h>|
|**fputws**|\<stdio.h> 或 \<wchar.h>|

通用 Windows 平台 (UWP) 应用中不支持控制台。 与控制台关联的标准流句柄 —**stdin**， **stdout**，并**stderr**— C 运行时函数可以在 UWP 应用中使用它们之前，必须重定向. 有关其他兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_fputs.c
// This program uses fputs to write
// a single line to the stdout stream.

#include <stdio.h>

int main( void )
{
   fputs( "Hello world from fputs.\n", stdout );
}
```

```Output
Hello world from fputs.
```

## <a name="see-also"></a>请参阅

[流 I/O](../../c-runtime-library/stream-i-o.md)<br/>
[fgets、fgetws](fgets-fgetws.md)<br/>
[gets、_getws](../../c-runtime-library/gets-getws.md)<br/>
[puts、_putws](puts-putws.md)<br/>
