---
title: _mkdir、_wmkdir
ms.date: 11/04/2016
apiname:
- _wmkdir
- _mkdir
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
- api-ms-win-crt-filesystem-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _mkdir
- tmkdir
- _tmkdir
- wmkdir
- _wmkdir
helpviewer_keywords:
- _wmkdir function
- folders [C++], creating
- wmkdir function
- directories [C++], creating
- mkdir function
- tmkdir function
- _mkdir function
- _tmkdir function
ms.assetid: 7f22d01d-63a5-4712-a6e7-d34878b2d840
ms.openlocfilehash: 0d89e1f0930cf9131156a4691069f1f17c15c124
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62285192"
---
# <a name="mkdir-wmkdir"></a>_mkdir、_wmkdir

新建目录。

## <a name="syntax"></a>语法

```C

int _mkdir(
   const char *dirname
);
int _wmkdir(
   const wchar_t *dirname
);
```

### <a name="parameters"></a>参数

*dirname*<br/>
新目录的路径。

## <a name="return-value"></a>返回值

如果创建新目录，这些函数都将返回值 0。 出现错误，函数将返回-1 和集**errno** ，如下所示。

**EEXIST**不创建目录，因为*dirname*是现有文件、 目录或设备的名称。

**ENOENT**找不到路径。

有关这些属性和其他的更多信息返回代码示例，请参见 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>备注

**_Mkdir**函数创建一个新目录具有指定*dirname。* **_mkdir**可以创建一个新目录，每次调用，因此，只有最后一个组件的*dirname*可以命名新目录。 **_mkdir**不会转换路径分隔符。 在 Windows NT 中，反斜杠 (\\) 和正斜杠 (/) 在运行时例程中都是字符串的有效路径分隔符。

**_wmkdir**是宽字符版本 **_mkdir**; *dirname*参数 **_wmkdir**是宽字符字符串。 **_wmkdir**并 **_mkdir**行为相同。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|Tchar.h 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tmkdir**|**_mkdir**|**_mkdir**|**_wmkdir**|

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_mkdir**|\<direct.h>|
|**_wmkdir**|\<direct.h> 或 \<wchar.h>|

有关更多兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>库

[C 运行时库](../../c-runtime-library/crt-library-features.md)的所有版本。

## <a name="example"></a>示例

```C
// crt_makedir.c

#include <direct.h>
#include <stdlib.h>
#include <stdio.h>

int main( void )
{
   if( _mkdir( "\\testtmp" ) == 0 )
   {
      printf( "Directory '\\testtmp' was successfully created\n" );
      system( "dir \\testtmp" );
      if( _rmdir( "\\testtmp" ) == 0 )
        printf( "Directory '\\testtmp' was successfully removed\n"  );
      else
         printf( "Problem removing directory '\\testtmp'\n" );
   }
   else
      printf( "Problem creating directory '\\testtmp'\n" );
}
```

### <a name="sample-output"></a>示例输出

```Output
Directory '\testtmp' was successfully created
Volume in drive C has no label.
Volume Serial Number is E078-087A

Directory of C:\testtmp

02/12/2002  09:56a      <DIR>          .
02/12/2002  09:56a      <DIR>          ..
               0 File(s)              0 bytes
               2 Dir(s)  15,498,690,560 bytes free
Directory '\testtmp' was successfully removed
```

## <a name="see-also"></a>请参阅

[目录控制](../../c-runtime-library/directory-control.md)<br/>
[_chdir、_wchdir](chdir-wchdir.md)<br/>
[_rmdir、_wrmdir](rmdir-wrmdir.md)<br/>
