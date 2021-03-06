---
title: _fputchar、_fputwchar
ms.date: 11/04/2016
apiname:
- _fputchar
- _fputwchar
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
- fputtchar
- _fputwchar
- fputwchar
- _fputtchar
- fputchar
- _fputchar
helpviewer_keywords:
- fputchar function
- standard output, writing to
- _fputtchar function
- fputwchar function
- _fputwchar function
- fputtchar function
- _fputchar function
ms.assetid: b92ff600-a924-4f2b-b0e7-3097ee31bdff
ms.openlocfilehash: 57ec2350fa1d0b681c6eed0c4cfc4ec4660977e8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62287925"
---
# <a name="fputchar-fputwchar"></a>_fputchar、_fputwchar

将字符写入 **stdout**。

## <a name="syntax"></a>语法

```C
int _fputchar(
   int c
);
wint_t _fputwchar(
   wchar_t c
);
```

### <a name="parameters"></a>参数

*c*<br/>
要写入的字符。

## <a name="return-value"></a>返回值

其中每个函数都会返回写入的字符。 有关 **_fputchar**，返回值为**EOF**指示错误。 有关 **_fputwchar**，返回值为**WEOF**指示错误。 如果 c **NULL**，这些函数将生成无效的参数异常，如中所述[参数验证](../../c-runtime-library/parameter-validation.md)。 如果允许执行继续，它们将返回**EOF** (或**WEOF**) 并设置**errno**到**EINVAL**。

有关这些及其他错误代码的详细信息，请参阅 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>备注

这两个函数将单个字符写入*c*到**stdout** ，并将提升为相应的指示符。 **_fputchar**等效于`fputc( stdout )`。 它还等效于**putchar**，但仅作为函数，而不是作为函数和宏实现。 与不同**fputc**并**putchar**，这些函数都不符合 ANSI 标准。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|Tchar.h 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_fputtchar**|**_fputchar**|**_fputchar**|**_fputwchar**|

## <a name="requirements"></a>要求

|函数|必需的标头|
|--------------|---------------------|
|**_fputchar**|\<stdio.h>|
|**_fputwchar**|\<stdio.h> 或 \<wchar.h>|

通用 Windows 平台 (UWP) 应用中不支持控制台。 与控制台关联的标准流句柄 —**stdin**， **stdout**，并**stderr**— C 运行时函数可以在 UWP 应用中使用它们之前，必须重定向. 有关更多兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_fputchar.c
// This program uses _fputchar
// to send a character array to stdout.

#include <stdio.h>

int main( void )
{
    char strptr[] = "This is a test of _fputchar!!\n";
    char *p = NULL;

    // Print line to stream using _fputchar.
    p = strptr;
    while( (*p != '\0') && _fputchar( *(p++) ) != EOF )
      ;
}
```

```Output
This is a test of _fputchar!!
```

## <a name="see-also"></a>请参阅

[流 I/O](../../c-runtime-library/stream-i-o.md)<br/>
[fgetc、fgetwc](fgetc-fgetwc.md)<br/>
[putc、putwc](putc-putwc.md)<br/>
