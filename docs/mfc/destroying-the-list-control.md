---
title: 销毁列表控件
ms.date: 11/04/2016
helpviewer_keywords:
- list controls [MFC], destroying
- CListCtrl class [MFC], destroying controls
ms.assetid: 513ec820-3a02-49d2-b073-a6a7a3fc91b3
ms.openlocfilehash: 963da9e6db2f0fe063dee1ca19ab23f545ed5e76
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62392878"
---
# <a name="destroying-the-list-control"></a>销毁列表控件

如果在嵌入你[CListCtrl](../mfc/reference/clistctrl-class.md)对象的视图或对话框类中，数据成员作为其所有者被销毁时销毁它。 如果您使用[CListView](../mfc/reference/clistview-class.md)，在销毁视图，框架将销毁控件。

如果您安排将某些列表数据存储在应用程序中而不是列表控件中，则需要安排释放。 有关详细信息，请参阅[回调项和回调掩码](/windows/desktop/Controls/using-list-view-controls)Windows SDK 中。

此外，您还要负责释放由您创建并与列表控件对象关联的任何图像列表。

## <a name="see-also"></a>请参阅

[使用 CListCtrl](../mfc/using-clistctrl.md)<br/>
[控件](../mfc/controls-mfc.md)
