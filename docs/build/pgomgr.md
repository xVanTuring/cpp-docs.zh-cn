---
title: pgomgr
ms.date: 03/14/2018
helpviewer_keywords:
- pgomgr program
- profile-guided optimizations, pgomgr
ms.assetid: 74589126-df18-42c9-8739-26d60e148d6a
ms.openlocfilehash: 4e3eb08c88db9d0ed4e47649014a600c3e0ccb78
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62295226"
---
# <a name="pgomgr"></a>pgomgr

将配置文件数据从一个或多个.pgc 文件添加到该.pgd 文件。

## <a name="syntax"></a>语法

> **pgomgr** [*options*] *pgcfiles* *pgdfile*

### <a name="parameters"></a>参数

*options*<br/>
以下选项可以指定给**pgomgr**:

-  或   显示可用**pgomgr**选项。

- **清除/** 导致要清除的所有配置文件信息的.pgd 文件。 不能指定.pgc 文件何时 **/clear**指定。

- **/detail**显示详细的统计信息，包括流关系图的覆盖率信息。

- **/summary**显示每个函数的统计信息。

- **/ 唯一**一起使用时 **/summary**，原因修饰函数名以显示。 默认值，当 **/ 唯一**未使用时，是要显示的未修饰的函数名称的。

- **/merge**\[**:**<em>n</em>] 导致要添加到该.pgd 文件的.pgc 文件中的数据。 可选参数*n*，允许您指定的数据应该添加*n*时间。 例如，如果一种方案通常是已完成的六倍反映何种频率通过客户，您可以在测试运行中一次执行并将其添加到该.pgd 文件六次与**pgomgr /merge:6**。

*pgcfiles*<br/>
一个或多个.pgc 文件，你想要合并到.pgd 文件的配置文件数据。 您可以指定单个.pgc 文件或多个.pgc 文件。 如果未指定任何的.pgc 文件， **pgomgr**合并所有其文件名将与.pgd 文件相同的.pgc 文件。

*pgdfile*<br/>
.Pgd 文件到其中要合并的.pgc 文件中的数据。

## <a name="remarks"></a>备注

> [!NOTE]
> 只能从 Visual Studio 开发人员命令提示符启动此工具。 无法从系统命令提示符或文件资源管理器中启动它。

## <a name="example"></a>示例

此示例命令清除 myapp.pgd 文件的配置文件数据：

`pgomgr /clear myapp.pgd`

此示例命令将添加配置文件数据中 myapp1.pgc.pgd 文件到三次：

`pgomgr /merge:3 myapp1.pgc myapp.pgd`

在此示例中，所有 myapp #.pgc 文件中的配置文件数据添加到 myapp.pgd 文件。

`pgomgr -merge myapp1.pgd`

## <a name="see-also"></a>请参阅

[按配置文件优化](profile-guided-optimizations.md)<br/>
[PgoAutoSweep](pgoautosweep.md)<br/>
[pgosweep](pgosweep.md)<br/>
