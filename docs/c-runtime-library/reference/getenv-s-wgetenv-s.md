---
title: getenv_s、_wgetenv_s
ms.date: 11/04/2016
apiname:
- getenv_s
- _wgetenv_s
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
- api-ms-win-crt-environment-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- getenv_s
- _tgetenv_s
- _wgetenv_s
helpviewer_keywords:
- _tgetenv_s function
- wgetenv_s function
- _wgetenv_s function
- getenv_s function
- environment variables
- tgetenv_s function
ms.assetid: c3ae1ffe-d4cd-4bae-bcb1-3afa754c613a
ms.openlocfilehash: eac3c036e2f4f271c7bc2d77c8ae82bec28d3617
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62331735"
---
# <a name="getenvs-wgetenvs"></a>getenv_s、_wgetenv_s

从当前环境中获取值。 这些版本的 [getenv、_wgetenv](getenv-wgetenv.md) 具有安全增强功能，如 [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)所述。

> [!IMPORTANT]
> 此 API 不能用于在 Windows 运行时中执行的应用程序。 有关详细信息，请参阅[通用 Windows 平台应用中不支持的 CRT 函数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)。

## <a name="syntax"></a>语法

```C
errno_t getenv_s(
   size_t *pReturnValue,
   char* buffer,
   size_t numberOfElements,
   const char *varname
);
errno_t _wgetenv_s(
   size_t *pReturnValue,
   wchar_t *buffer,
   size_t numberOfElements,
   const wchar_t *varname
);
template <size_t size>
errno_t getenv_s(
   size_t *pReturnValue,
   char (&buffer)[size],
   const char *varname
); // C++ only
template <size_t size>
errno_t _wgetenv_s(
   size_t *pReturnValue,
   wchar_t (&buffer)[size],
   const wchar_t *varname
); // C++ only
```

### <a name="parameters"></a>参数

*pReturnValue*<br/>
所需的缓冲区大小，如果找不到该变量，则为 0。

*buffer*<br/>
用于存储环境变量值的缓冲区。

*numberOfElements*<br/>
大小*缓冲区*。

*varname*<br/>
环境变量名称。

## <a name="return-value"></a>返回值

如果成功，则为零；如果失败，则返回错误代码。

### <a name="error-conditions"></a>错误条件

|*pReturnValue*|*buffer*|*numberOfElements*|*varname*|返回值|
|--------------------|--------------|------------------------|---------------|------------------|
|**NULL**|任何|任何|任何|**EINVAL**|
|任何|**NULL**|>0|任何|**EINVAL**|
|任何|任何|任何|**NULL**|**EINVAL**|

如[参数验证](../../c-runtime-library/parameter-validation.md)中所述，这些错误条件调用无效参数处理程序。 如果允许执行继续，则函数将设置**errno**到**EINVAL**并返回**EINVAL**。

此外，如果缓冲区太小，这些函数将返回**ERANGE**。 它们不会调用无效的参数处理程序。 它们是写出所需的缓冲区大小，以*pReturnValue*，从而使程序以使用较大的缓冲区再次调用函数。

## <a name="remarks"></a>备注

**Getenv_s**函数的环境变量列表中搜索*varname*。 **getenv_s**不区分大小写，在 Windows 操作系统中。 **getenv_s**并[_putenv_s](putenv-s-wputenv-s.md)使用由全局变量指向该环境的副本 **_environ**来访问该环境。 **getenv_s**操作仅在运行时库访问的数据结构和不能在环境"段"为该进程创建的操作系统。 因此，程序使用*envp*自变量[主要](../../cpp/main-program-startup.md)或[wmain](../../cpp/main-program-startup.md)可能会检索无效信息。

**_wgetenv_s**是宽字符版本**getenv_s**; 的自变量和返回值 **_wgetenv_s**都是宽字符字符串。 **_Wenviron**全局变量是宽字符版本 **_environ**。

在 MBCS 程序中 （例如，在 SBCS ASCII 程序中）， **_wenviron**最初**NULL**因为环境多字节字符字符串组成。 然后，在首次调用[_wputenv](putenv-wputenv.md)，或在首次调用 **_wgetenv_s**，如果 (MBCS) 环境已存在，创建并通过指向相应的宽字符字符串环境 **_wenviron**。

同样，在 Unicode (**_wmain**) 程序中， **_environ**最初**NULL**因为环境宽字符字符串组成。 然后，在首次调用[_putenv](putenv-wputenv.md)，或在首次调用**getenv_s**如果 (Unicode) 环境已存在，创建并通过指向相应的 MBCS 环境 **_environ**。

当程序中同时存在环境的两个副本（MBCS 和 Unicode）时，运行时系统必须保留这两个副本，而这将减慢执行时间。 例如，当您调用 **_putenv**，调用 **_wputenv**还自动执行，以便两个环境字符串相对应。

> [!CAUTION]
> 在极少数情况下，当运行时系统同时保留环境的 Unicode 版本和多字节版本时，两个环境版本可能不完全对应。 这是因为，虽然任何唯一的多字节字符字符串将映射到唯一的 Unicode 字符串，但从唯一的 Unicode 字符串到多字节字符字符串的映射却不一定是唯一的。 有关详细信息，请参阅 [_environ、_wenviron](../../c-runtime-library/environ-wenviron.md)。

> [!NOTE]
> **_Putenv_s**并 **_getenv_s**系列函数不是线程安全。 **_getenv_s**返回时字符串指针 **_putenv_s**修改字符串，从而导致随机失败。 确保对这些函数的调用同步。

在 C++ 中，这些函数的使用由模板重载简化；重载可以自动推导出缓冲区长度，从而不再需要指定大小自变量。 有关详细信息，请参阅[安全模板重载](../../c-runtime-library/secure-template-overloads.md)。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tgetenv_s**|**getenv_s**|**getenv_s**|**_wgetenv_s**|

若要检查或更改的值**TZ**环境变量，使用**getenv_s**， **_putenv**，以及 **_tzset**、 所需的方式。 有关详细信息**TZ**，请参阅[_tzset](tzset.md)并[_daylight、 _dstbias、 _timezone 和 _tzname](../../c-runtime-library/daylight-dstbias-timezone-and-tzname.md)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**getenv_s**|\<stdlib.h>|
|**_wgetenv_s**|\<stdlib.h> 或 \<wchar.h>|

有关其他兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_getenv_s.c
// This program uses getenv_s to retrieve
// the LIB environment variable and then uses
// _putenv to change it to a new value.

#include <stdlib.h>
#include <stdio.h>

int main( void )
{
   char* libvar;
   size_t requiredSize;

   getenv_s( &requiredSize, NULL, 0, "LIB");
   if (requiredSize == 0)
   {
      printf("LIB doesn't exist!\n");
      exit(1);
   }

   libvar = (char*) malloc(requiredSize * sizeof(char));
   if (!libvar)
   {
      printf("Failed to allocate memory!\n");
      exit(1);
   }

   // Get the value of the LIB environment variable.
   getenv_s( &requiredSize, libvar, requiredSize, "LIB" );

   printf( "Original LIB variable is: %s\n", libvar );

   // Attempt to change path. Note that this only affects
   // the environment variable of the current process. The command
   // processor's environment is not changed.
   _putenv_s( "LIB", "c:\\mylib;c:\\yourlib" );

   getenv_s( &requiredSize, NULL, 0, "LIB");

   libvar = (char*) realloc(libvar, requiredSize * sizeof(char));
   if (!libvar)
   {
      printf("Failed to allocate memory!\n");
      exit(1);
   }

   // Get the new value of the LIB environment variable.
   getenv_s( &requiredSize, libvar, requiredSize, "LIB" );

   printf( "New LIB variable is: %s\n", libvar );

   free(libvar);
}
```

```Output
Original LIB variable is: c:\vctools\lib;c:\vctools\atlmfc\lib;c:\vctools\PlatformSDK\lib;c:\vctools\Visual Studio SDKs\DIA Sdk\lib;c:\vctools\Visual Studio SDKs\BSC Sdk\lib
New LIB variable is: c:\mylib;c:\yourlib
```

## <a name="see-also"></a>请参阅

[进程和环境控制](../../c-runtime-library/process-and-environment-control.md)<br/>
[环境常量](../../c-runtime-library/environmental-constants.md)<br/>
[_putenv、_wputenv](putenv-wputenv.md)<br/>
[_dupenv_s、_wdupenv_s](dupenv-s-wdupenv-s.md)<br/>
