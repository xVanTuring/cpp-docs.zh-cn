---
title: push_macro
ms.date: 11/04/2016
f1_keywords:
- vc-pragma.push_macro
- push_macro_CPP
helpviewer_keywords:
- pragmas, push_macro
- push_macro pragma
ms.assetid: ac89efc9-afd1-4dfe-bfd1-497229b3e81d
ms.openlocfilehash: 5602dd91b7d017c49a122524e469100b0ec6debf
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62179823"
---
# <a name="pushmacro"></a>push_macro
将值保存*macro_name*为此宏堆栈顶部的宏。

## <a name="syntax"></a>语法

```
#pragma push_macro("
macro_name
")
```

## <a name="remarks"></a>备注

可以检索的值*macro_name*与`pop_macro`。

请参阅[pop_macro](../preprocessor/pop-macro.md)有关的示例。

## <a name="see-also"></a>请参阅

[Pragma 指令和 __Pragma 关键字](../preprocessor/pragma-directives-and-the-pragma-keyword.md)