---
title: CL 命令文件
ms.date: 11/04/2016
f1_keywords:
- cl
helpviewer_keywords:
- cl.exe compiler, command files
- command files
- command files, CL compiler
ms.assetid: ec3cea06-2af0-4fe9-a94c-119c9d31b3a9
ms.openlocfilehash: 9810f7b4308eab2b47a068072039335e59e19f5f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62272580"
---
# <a name="cl-command-files"></a>CL 命令文件

命令文件是包含选项和文件名，否则应键入的文本文件[命令行](compiler-command-line-syntax.md)或使用指定[CL 环境变量](cl-environment-variables.md)。 CL 接受作为参数在 CL 环境变量或命令行编译器命令文件。 与命令行或 CL 环境变量不同，命令文件允许使用多行选项和文件名。

根据命令文件名 CL 环境变量中或命令行上的位置处理选项和命令文件中的文件名。 但是，如果 /link 选项出现在命令文件，在行的其余部分上的所有选项都传递给链接器。 命令文件中的后续行中的选项和命令文件调用后的在命令行选项仍属编译器选项。 有关选项的顺序将如何影响其解释的详细信息，请参阅[CL 选项的顺序](order-of-cl-options.md)。

命令文件不得包含 CL 命令。 每个选项必须开始和结束的同一行;不能使用反斜杠 (**\\**) 若要跨两个行合并选项。

指定命令文件 at 符号 (**\@**) filename; 后跟文件名可以指定绝对或相对路径。

例如，如果以下命令在名为响应的文件：

```
/Og /link LIBC.LIB
```

指定以下 CL 命令：

```
CL /Ob2 @RESP MYAPP.C
```

改为 CL 命令如下所示：

```
CL /Ob2 /Og MYAPP.C /link LIBC.LIB
```

请注意，有效地组合命令行和命令文件命令。

## <a name="see-also"></a>请参阅

[MSVC 编译器命令行语法](compiler-command-line-syntax.md)<br/>
[MSVC 编译器选项](compiler-options.md)
