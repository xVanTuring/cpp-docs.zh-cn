---
title: 如何：调试发行版本
ms.date: 11/04/2016
helpviewer_keywords:
- debugging [C++], release builds
- release builds, debugging
ms.assetid: d333e4d1-4e6c-4384-84a9-cb549702da25
ms.openlocfilehash: 6d93fac4e980085c322acb55e6f8758e6cea0a00
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62188954"
---
# <a name="how-to-debug-a-release-build"></a>如何：调试发行版本

您可以调试发行版本的应用程序。

### <a name="to-debug-a-release-build"></a>若要调试发行版本

1. 打开**属性页**项目对话框。 有关详细信息，请参阅[设置C++Visual Studio 中的编译器和生成属性](working-with-project-properties.md)。

1. 单击**C /C++** 节点。 设置**调试信息格式**到[C7 兼容 (/ Z7)](reference/z7-zi-zi-debug-information-format.md)或**程序数据库 (/Zi)**。

1. 展开**链接器**然后单击**常规**节点。 设置**启用增量链接**到[否 (/ /INCREMENTAL: NO)](reference/incremental-link-incrementally.md)。

1. 选择**调试**节点。 设置**生成调试信息一样**到[是 (/debug)](reference/debug-generate-debug-info.md)。

1. 选择**优化**节点。 设置**引用**到[/opt: ref](reference/opt-optimizations.md)并**启用 COMDAT 折叠**到[/opt: icf](reference/opt-optimizations.md)。

1. 现在可以调试版本生成应用程序。 若要发现问题，单步执行代码 （或使用实时中调试），直到找到失败发生的位置，然后确定不正确的参数或代码。

   如果应用程序可在调试版本中，但在发行版本中失败，其中一个的编译器优化可能会公开的源代码中的一个缺陷。 若要隔离此问题，禁用为每个源代码文件选择的优化，直到您找到该文件，导致问题的优化。 （若要加快该过程，可以将文件划分为两个组，禁用优化的一个组，并在组中，找到问题后继续如此划分，直到找到问题文件。）

   可以使用[/RTC](reference/rtc-run-time-error-checks.md)尝试公开您的调试版本中的此类 bug。

   有关详细信息，请参阅[优化您的代码](optimizing-your-code.md)。

## <a name="see-also"></a>请参阅

[修复发行版本问题](fixing-release-build-problems.md)
