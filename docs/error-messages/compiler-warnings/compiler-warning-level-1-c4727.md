---
title: 编译器警告（等级 1）C4727
ms.date: 11/04/2016
f1_keywords:
- C4727
helpviewer_keywords:
- C4727
ms.assetid: 991b0087-3a50-40f5-9cdb-cdc367cd472c
ms.openlocfilehash: be1a248fc2709706e137b543344966735c19064e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62386429"
---
# <a name="compiler-warning-level-1-c4727"></a>编译器警告（等级 1）C4727

"PCH 名 pch_file 为具有相同时间戳 obj_file_1 和 obj_file_2 中找到。  使用第一个 PCH。

编译与多个编译单位时发生 C4727 **/Yc**，和编译器就能够将所有.obj 文件具有相同的.pch 时间戳都标记。

若要解决，编译一个源文件 **/Yc /c** （创建 pch） 和其他使用单独编译 **/Yu /c** （使用 pch），然后将它们链接在一起。

因此，如果了以下并生成 C4727:

**cl /clr /GL a.cpp b.cpp c.cpp /Ycstdafx.h**

您将执行以下步骤改为：

**cl /clr /GL a.cpp /Ycstdafx.h /c**

**cl /clr /GL b.cpp c.cpp /Yustdafx.h /link a.obj**

有关详细信息，请参见

- [/Yc（创建预编译标头文件）](../../build/reference/yc-create-precompiled-header-file.md)

- [/Yu（使用预编译标头文件）](../../build/reference/yu-use-precompiled-header-file.md)