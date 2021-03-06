---
title: 控件条类
ms.date: 11/04/2016
f1_keywords:
- vc.classes.control
helpviewer_keywords:
- control bars [MFC], classes
ms.assetid: 11009103-cad8-4309-85ce-3d2e858e1818
ms.openlocfilehash: 3426d84eab888a6fe78b663945776fff2fe708dd
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301950"
---
# <a name="control-bar-classes"></a>控件条类

控件条附加到框架窗口。 它们包含按钮、 状态窗格或对话框模板。 通过将附加到实现自由浮动的控件条，也称为工具调色板[CMiniFrameWnd](../mfc/reference/cminiframewnd-class.md)对象。

## <a name="framework-control-bars"></a>框架控件条

这些控件条是 MFC 框架的重要组成部分。 它们是易于使用和不是 Windows 控件条，由于集成了框架功能更强大。 大多数 MFC 应用程序使用这些控件条，而不是 Windows 控件条。

[CControlBar](../mfc/reference/ccontrolbar-class.md)<br/>
本部分中列出的 MFC 控件条的基类。 控件条是窗口框架窗口的边缘对齐。 控件条包含`HWND`-基于子控件或控件不基于`HWND`，如工具栏按钮。

[CDialogBar](../mfc/reference/cdialogbar-class.md)<br/>
一个基于对话框模板的控件条。

[CReBar](../mfc/reference/crebar-class.md)<br/>
支持一个工具栏，它可以包含其他子窗口的控件的窗体。

[CToolBar](../mfc/reference/ctoolbar-class.md)<br/>
不包含命令的位图按钮的工具栏控件窗口根据`HWND`。 大多数 MFC 应用程序使用此类而不是`CToolBarCtrl`。

[CStatusBar](../mfc/reference/cstatusbar-class.md)<br/>
状态栏控件窗口的基类。 大多数 MFC 应用程序使用此类而不是`CStatusBarCtrl`。

## <a name="windows-control-bars"></a>Windows 控件条

这些控件条是瘦包装相应的 Windows 控件。 由于未集成了框架，就越难以使用比上面列出的控件条。 大多数 MFC 应用程序使用前面列出的控件条。

[CRebarCtrl](../mfc/reference/crebarctrl-class.md)<br/>
实现内部的控件`CRebar`对象。

[CStatusBarCtrl](../mfc/reference/cstatusbarctrl-class.md)<br/>
水平窗口中，通常分为的窗格，在其中应用程序可显示状态信息。

[CToolBarCtrl](../mfc/reference/ctoolbarctrl-class.md)<br/>
提供 Windows 工具栏公共控件的功能。

## <a name="related-classes"></a>相关的类

[CToolTipCtrl](../mfc/reference/ctooltipctrl-class.md)<br/>
一个小型的弹出窗口，显示的文本来描述应用程序中工具用途的单行。

[CDockState](../mfc/reference/cdockstate-class.md)<br/>
处理停靠控件条的状态数据持久的存储。

## <a name="see-also"></a>请参阅

[类概述](../mfc/class-library-overview.md)
