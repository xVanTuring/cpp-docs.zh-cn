---
title: lrint、lrintf、lrintl、llrint、llrintf、llrintl
ms.date: 04/05/2018
apiname:
- lrint
- lrintl
- lrintf
- llrint
- llrintf
- llrintl
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
- api-ms-win-crt-math-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- lrint
- lrintf
- lrintl
- llrint
- llrintf
- llrintl
- math/lrint
- math/lrintf
- math/lrintl
- math/llrint
- math/llrintf
- math/llrintl
helpviewer_keywords:
- lrint function
- lrintf function
- lrintl function
- llrint function
- llrintf function
- llrintl function
ms.assetid: 28ccd5b3-5e6f-434f-997d-a21d51b8ce7f
ms.openlocfilehash: 01680a62e654112475a55bd8eac0cc14d254e2a2
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62285767"
---
# <a name="lrint-lrintf-lrintl-llrint-llrintf-llrintl"></a>lrint、lrintf、lrintl、llrint、llrintf、llrintl

使用当前舍入模式和方向将指定浮点值舍入到最接近的整数值。

## <a name="syntax"></a>语法

```C
long int lrint(
   double x
);

long int lrint(
   float x
); //C++ only

long int lrint(
   long double x
); //C++ only

long int lrintf(
   float x
);

long int lrintl(
   long double x
);

long long int llrint(
   double x
);

long long int llrint(
   float x
); //C++ only

long long int llrint(
   long double x
); //C++ only

long long int llrintf(
   float x
);

long long int llrintl(
   long double x
);
```

### <a name="parameters"></a>参数

*x*<br/>
要舍入的值。

## <a name="return-value"></a>返回值

如果成功，返回的圆角的整数值*x*。

|问题|返回|
|-----------|------------|
|*x*超出返回类型的范围<br /><br /> *x* = ±∞<br /><br /> *x* = NaN|将引发**FE_INVALID** ，并返回零 (0)。|

## <a name="remarks"></a>备注

因为C++允许重载，可以调用的重载**lrint**并**llrint**采用**float**并**长** **双**类型。 在 C 程序中， **lrint**并**llrint**始终采用**double**。

如果*x*不表示等效的整数值，这些函数将引发浮**FE_INEXACT**。

**特定于 Microsoft**:结果超出范围时的返回类型，或当参数为 NaN 或无穷大，返回值是定义的实现。 Microsoft 编译器返回零 (0) 值。

## <a name="requirements"></a>要求

|函数|C 标头|C++ 标头|
|--------------|--------------|------------------|
|**lrint**， **lrintf**， **lrintl**， **llrint**， **llrintf**， **llrintl**|\<math.h>|\<cmath>|

有关其他兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>请参阅

[按字母顺序的函数参考](crt-alphabetical-function-reference.md)<br/>
