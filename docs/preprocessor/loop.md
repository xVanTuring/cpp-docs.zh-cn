---
title: 循环
ms.date: 10/18/2018
f1_keywords:
- loop_CPP
- vc-pragma.loop
ms.assetid: 6d5bb428-cead-47e7-941d-7513bbb162c7
ms.openlocfilehash: a1640881d98073381a941478f4b78177a95698d7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62411326"
---
# <a name="loop"></a>循环

控制自动并行化如何考虑循环代码和/或从自动向量化进行的考虑中排除循环。

## <a name="syntax"></a>语法

```
#pragma loop( hint_parallel(n) )
#pragma loop( no_vector )
#pragma loop( ivdep )
```

### <a name="parameters"></a>参数

*hint_parallel(n)*<br/>
对跨应并行化此循环的编译器的提示*n*线程，其中*n*正整数文本或零。 如果*n*为零，在运行时使用的最大线程数。 这是对编译器的提示而不是命令，并且并不保证会并行化循环。 如果循环具有数据依赖项或结构问题，例如，循环存储到在循环体外使用的标量，则将不会并行化循环。

编译器将忽略此选项，除非[/Qpar](../build/reference/qpar-auto-parallelizer.md)指定编译器开关。

*no_vector*<br/>
默认情况下，自动向量化处于启用状态，并且将尝试向量化其计算为从中受益的所有循环。 请指定此杂注以对杂注后面的循环禁用自动向量化。

*ivdep*<br/>
对编译器忽略此循环的向量依赖项的提示。 结合使用这*hint_parallel*。

## <a name="remarks"></a>备注

若要使用**循环**杂注，之前将其置于 — 不在-循环定义。 杂注对它后面的循环的范围有效。 您可按任意顺序将多个杂注应用于一个循环，但必须在单独的杂注语句中声明每个杂注。

## <a name="see-also"></a>请参阅

[自动并行化和自动矢量化](../parallel/auto-parallelization-and-auto-vectorization.md)<br/>
[Pragma 指令和 __Pragma 关键字](../preprocessor/pragma-directives-and-the-pragma-keyword.md)