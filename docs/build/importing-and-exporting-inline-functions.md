---
title: 导入和导出内联函数
ms.date: 11/04/2016
helpviewer_keywords:
- exporting functions [C++], inline functions
- inline functions [C++], importing
- DLLs [C++], importing
- importing functions [C++]
- DLLs [C++], exporting from
- importing inline functions [C++]
- inline functions [C++], exporting
- functions [C++], importing
- functions [C++], exporting
ms.assetid: 89f488f8-b078-40fe-afd7-80bd7840057b
ms.openlocfilehash: ed523d84228124d4a8d99e443c0c744f362f1c56
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62273438"
---
# <a name="importing-and-exporting-inline-functions"></a>导入和导出内联函数

可以为内联定义导入的函数。 效果大致是相同定义标准函数内联;对函数的调用会展开为内联代码，类似于宏。 这是主要用作一种方法支持C++可能的内嵌某些成员函数以提高效率的 DLL 中的类。

导入的内联函数的一个功能是，您可以采用其地址C++。 编译器返回的副本驻留在 DLL 中的内联函数的地址。 导入的内联函数的另一个功能是函数的可以初始化静态本地数据的导入，与全局导入的数据不同。

> [!CAUTION]
>  在提供导入内联函数，因为他们可以创建可能发生版本冲突时应十分小心。 内联函数获取扩展为应用程序代码;因此，如果您更高版本重写函数，它不会更新除非重新编译应用程序本身。 （通常情况下，DLL 函数可以更新而重新生成的应用程序使用它们。）

## <a name="what-do-you-want-to-do"></a>你希望做什么？

- [从 DLL 导出](exporting-from-a-dll.md)

- [导出从 DLL 使用。DEF 文件](exporting-from-a-dll-using-def-files.md)

- [使用 __declspec （dllexport） 从 DLL 导出](exporting-from-a-dll-using-declspec-dllexport.md)

- [导出和导入使用 AFX_EXT_CLASS](exporting-and-importing-using-afx-ext-class.md)

- [导出C++函数以用于 C 语言可执行文件](exporting-cpp-functions-for-use-in-c-language-executables.md)

- [确定要使用的导出方法](determining-which-exporting-method-to-use.md)

- [使用 __declspec(dllimport) 导入到应用程序中](importing-into-an-application-using-declspec-dllimport.md)

## <a name="see-also"></a>请参阅

[导入和导出](importing-and-exporting.md)
