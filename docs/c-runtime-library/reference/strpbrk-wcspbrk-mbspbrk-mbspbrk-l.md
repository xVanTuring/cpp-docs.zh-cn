---
title: strpbrk、wcspbrk、_mbspbrk、_mbspbrk_l
ms.date: 11/04/2016
apiname:
- _mbspbrk
- wcspbrk
- _mbspbrk_l
- strpbrk
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
- api-ms-win-crt-multibyte-l1-1-0.dll
- api-ms-win-crt-string-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _fstrpbrk
- _mbspbrk
- strpbrk
- _tcspbrk
- _ftcspbrk
- wcspbrk
helpviewer_keywords:
- fstrpbrk function
- _ftcspbrk function
- _mbspbrk_l function
- strpbrk function
- _fstrpbrk function
- mbspbrk function
- characters [C++], scanning strings
- _tcspbrk function
- wcspbrk function
- ftcspbrk function
- character sets [C++], scanning strings for characters
- strings [C++], scanning
- tcspbrk function
- _mbspbrk function
- mbspbrk_l function
ms.assetid: 80b504f7-a167-4dde-97ad-4ae3000dc810
ms.openlocfilehash: 059b0659a8088783c6d169288de486b41a6e8d82
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62209562"
---
# <a name="strpbrk-wcspbrk-mbspbrk-mbspbrkl"></a>strpbrk、wcspbrk、_mbspbrk、_mbspbrk_l

扫描字符串以查找指定字符集中的字符。

> [!IMPORTANT]
> `_mbspbrk` 和 `_mbspbrk_l` 无法用于在 Windows 运行时中执行的应用程序。 有关详细信息，请参阅[通用 Windows 平台应用中不支持的 CRT 函数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)。

## <a name="syntax"></a>语法

```C
char *strpbrk(
   const char *str,
   const char *strCharSet
); // C only
char *strpbrk(
   char *str,
   const char *strCharSet
); // C++ only
const char *strpbrk(
   const char *str,
   const char *strCharSet
); // C++ only
wchar_t *wcspbrk(
   const wchar_t *str,
   const wchar_t *strCharSet
); // C only
wchar_t *wcspbrk(
   wchar_t *str,
   const wchar_t *strCharSet
); // C++ only
const wchar_t *wcspbrk(
   const wchar_t *str,
   const wchar_t *strCharSet
); // C++ only
unsigned char *_mbspbrk(
   const unsigned char *str,
   const unsigned char *strCharSet
); // C only
unsigned char *_mbspbrk(
   unsigned char *str,
   const unsigned char *strCharSet
); // C++ only
const unsigned char *_mbspbrk(
   const unsigned char *str,
   const unsigned char *strCharSet
); // C++ only
unsigned char *_mbspbrk_l(
   const unsigned char *str,
   const unsigned char *strCharSet,
   _locale_t locale
); // C only
unsigned char *_mbspbrk_l(
   unsigned char *str,
   const unsigned char *strCharSet,
   _locale_t locale
); // C++ only
const unsigned char *_mbspbrk_l(
   const unsigned char *str,
   const unsigned char* strCharSet,
   _locale_t locale
); // C++ only
```

### <a name="parameters"></a>参数

*str*<br/>
null 终止的搜索字符串。

*strCharSet*<br/>
null 终止的字符集。

*locale*<br/>
要使用的区域设置。

## <a name="return-value"></a>返回值

返回指向从任何字符的第一个匹配项的指针*strCharSet*中*str*，或如果两个字符串参数的 NULL 指针的共同点没有字符。

## <a name="remarks"></a>备注

`strpbrk`函数中的字符的第一个匹配项返回一个指针*str*属于组中的字符*strCharSet*。 搜索不包括终止 null 字符。

`wcspbrk` 和 `_mbspbrk` 分别是 `strpbrk`的宽字符及多字节字符版本。 `wcspbrk` 的参数和返回值是宽字符字符串；而 `_mbspbrk` 的则是多字节字符字符串。

`_mbspbrk` 会验证其参数。 如果*str*或*strCharSet*为 NULL，将调用无效参数处理程序，如中所述[参数验证](../../c-runtime-library/parameter-validation.md)。 如果允许执行继续，则`_mbspbrk`返回 NULL，并设置`errno`EINVAL 到。 `strpbrk` 和 `wcspbrk` 不会验证其参数。 否则这三个函数否则具有相同行为。

`_mbspbrk` 类似于 `_mbscspn`，只不过 `_mbspbrk` 返回一个指针，而不是 [size_t](../../c-runtime-library/standard-types.md) 类型的值。

在 C 中，这些函数采用**const**的第一个参数的指针。 在 C++ 中，有两个重载可用。 采用指向的重载**const**返回一个指向**const**; 将指针传递到非版本**const**返回一个指向非**常量**. 如果这两个定义宏 _CRT_CONST_CORRECT_OVERLOADS **const**和非-**const**提供了这些函数的版本。 如果需要非**const**两个行为C++重载，定义符号 _CONST_RETURN。

输出值受区域设置; 的 LC_CTYPE 类别设置的设置有关详细信息，请参阅[setlocale](setlocale-wsetlocale.md)。 无需这些函数的版本 **_l**后缀，请使用当前区域设置的区域设置相关的行为; 使用版本 **_l**后缀是完全相同，只不过它使用的区域设置参数改为传入。 有关详细信息，请参阅 [Locale](../../c-runtime-library/locale.md)。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|`_tcspbrk`|`strpbrk`|`_mbspbrk`|`wcspbrk`|
|**不适用**|**不适用**|`_mbspbrk_l`|**不适用**|

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|`strpbrk`|\<string.h>|
|`wcspbrk`|\<string.h> 或 \<wchar.h>|
|`_mbspbrk`， `_mbspbrk_l`|\<mbstring.h>|

有关兼容性的更多信息，请参见 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_strpbrk.c

#include <string.h>
#include <stdio.h>

int main( void )
{
   char string[100] = "The 3 men and 2 boys ate 5 pigs\n";
   char *result = NULL;

   // Return pointer to first digit in "string".
   printf( "1: %s\n", string );
   result = strpbrk( string, "0123456789" );
   printf( "2: %s\n", result++ );
   result = strpbrk( result, "0123456789" );
   printf( "3: %s\n", result++ );
   result = strpbrk( result, "0123456789" );
   printf( "4: %s\n", result );
}
```

```Output
1: The 3 men and 2 boys ate 5 pigs

2: 3 men and 2 boys ate 5 pigs

3: 2 boys ate 5 pigs

4: 5 pigs
```

## <a name="see-also"></a>请参阅

[字符串操作](../../c-runtime-library/string-manipulation-crt.md)<br/>
[区域设置](../../c-runtime-library/locale.md)<br/>
[多字节字符序列的解释](../../c-runtime-library/interpretation-of-multibyte-character-sequences.md)<br/>
[strcspn、wcscspn、_mbscspn、_mbscspn_l](strcspn-wcscspn-mbscspn-mbscspn-l.md)<br/>
[strchr、wcschr、_mbschr、_mbschr_l](strchr-wcschr-mbschr-mbschr-l.md)<br/>
[strrchr、wcsrchr、_mbsrchr、_mbsrchr_l](strrchr-wcsrchr-mbsrchr-mbsrchr-l.md)<br/>
