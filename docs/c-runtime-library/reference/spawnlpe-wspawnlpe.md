---
title: _spawnlpe、_wspawnlpe
ms.date: 11/04/2016
apiname:
- _spawnlpe
- _wspawnlpe
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
- api-ms-win-crt-process-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- spawnlpe
- _wspawnlpe
- _spawnlpe
- wspawnlpe
helpviewer_keywords:
- _wspawnlpe function
- wspawnlpe function
- processes, creating
- spawnlpe function
- _spawnlpe function
- processes, executing new
- process creation
ms.assetid: e171ebfa-70e7-4c44-8331-2a291fc17bd6
ms.openlocfilehash: fa390c039a3d663cb79cb311667e568a6a053131
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62355154"
---
# <a name="spawnlpe-wspawnlpe"></a>_spawnlpe、_wspawnlpe

创建并执行更新过程。

> [!IMPORTANT]
> 此 API 不能用于在 Windows 运行时中执行的应用程序。 有关详细信息，请参阅[通用 Windows 平台应用中不支持的 CRT 函数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)。

## <a name="syntax"></a>语法

```C
intptr_t _spawnlpe(
   int mode,
   const char *cmdname,
   const char *arg0,
   const char *arg1,
   ... const char *argn,
   NULL,
   const char *const *envp
);
intptr_t _wspawnlpe(
   int mode,
   const wchar_t *cmdname,
   const wchar_t *arg0,
   const wchar_t *arg1,
   ... const wchar_t *argn,
   NULL,
   const wchar_t *const *envp
);
```

### <a name="parameters"></a>参数

*模式*<br/>
调用进程的执行模式。

*cmdname*<br/>
要执行的文件的路径。

*arg0*， *arg1*，...*argn*<br/>
指向参数的指针的列表。 *Arg0*参数通常是一个指向*cmdname*。 自变量*arg1*通过*argn*是指向构成新参数列表的字符串。 遵循*argn*，必须有**NULL**指针，用以标记参数列表的末尾。

*envp*<br/>
指向环境设置的指针的数组。

## <a name="return-value"></a>返回值

从同步的返回值 **_spawnlpe**或 **_wspawnlpe** (**_P_WAIT**指定为*模式*) 是新的退出状态过程。 异步的返回值 **_spawnlpe**或 **_wspawnlpe** (**_P_NOWAIT**或者 **_P_NOWAITO**指定为*模式*) 是进程句柄。 如果进程正常终止，则退出状态为 0。 如果生成的进程专门使用非零参数调用时将退出状态设置为非零值**退出**例程。 如果更新过程未显式设置正退出状态，则正退出状态指示因中止或中断而造成的异常退出。 返回值-1 指示的错误 （未启动新进程）。 在这种情况下， **errno**设置为以下值之一。

|||
|-|-|
| **E2BIG** | 参数列表超过 1024 个字节。 |
| **EINVAL** | *模式*参数无效。 |
| **ENOENT** | 未找到文件或路径。 |
| **ENOEXEC** | 指定的文件不是可执行文件或者有无效的可执行文件格式。 |
| **ENOMEM** | 没有足够的内存可用于执行新进程。 |

有关这些代码及其他返回代码的详细信息，请参阅 [errno、_doserrno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>备注

其中每个函数都创建并执行一个新进程，将每个命令行自变量作为单独的参数进行传递，并将一个数组指针传递给环境设置。 这些函数将使用**路径**环境变量查找要执行的文件。

这些函数验证其参数。 如果任一*cmdname*或*arg0*是一个空字符串或 null 指针，无效参数处理程序调用，如中所述[参数验证](../../c-runtime-library/parameter-validation.md)。 如果允许继续执行，这些函数将设置**errno**到**EINVAL**，并返回-1。 不生成任何新进程。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_spawnlpe**|\<process.h>|
|**_wspawnlpe**|\<stdio.h> 或 \<wchar.h>|

有关更多兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

在参见 [_spawn、_wspawn 函数](../../c-runtime-library/spawn-wspawn-functions.md)中的示例。

## <a name="see-also"></a>请参阅

[进程和环境控制](../../c-runtime-library/process-and-environment-control.md)<br/>
[_spawn、_wspawn 函数](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
[abort](abort.md)<br/>
[atexit](atexit.md)<br/>
[_exec、_wexec 函数](../../c-runtime-library/exec-wexec-functions.md)<br/>
[exit、_Exit、_exit](exit-exit-exit.md)<br/>
[_flushall](flushall.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_onexit、_onexit_m](onexit-onexit-m.md)<br/>
[_setmbcp](setmbcp.md)<br/>
[system、_wsystem](system-wsystem.md)<br/>
