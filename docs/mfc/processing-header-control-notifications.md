---
title: 处理标题控件通知
ms.date: 11/04/2016
helpviewer_keywords:
- CHeaderCtrl class [MFC], processing notifications
- controls [MFC], header
- notifications [MFC], processing for CHeaderCtrl
- header controls [MFC], processing notifications
- header control notifications
ms.assetid: e6c6af7c-d458-4d33-85aa-48014ccde5f6
ms.openlocfilehash: 3c5d147741123f97a53b18a854db9204738d0a2f
ms.sourcegitcommit: c3093251193944840e3d0a068ecc30e6449624ba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2019
ms.locfileid: "57287682"
---
# <a name="processing-header-control-notifications"></a>处理标题控件通知

在视图或对话框类中，使用属性窗口创建[OnChildNotify](../mfc/reference/cwnd-class.md#onchildnotify)处理程序函数与 switch 语句的任何标头控件 ([CHeaderCtrl](../mfc/reference/cheaderctrl-class.md)) 到所需的通知消息处理 (请参阅[消息映射到函数](../mfc/reference/mapping-messages-to-functions.md))。 当用户单击或双击一个标头项，项，依次类推之间的分隔符的拖动时，将向父窗口发送通知。

与标头控件关联的通知消息中列出[标头控件引用](/windows/desktop/controls/header-control-reference)Windows SDK 中。

## <a name="see-also"></a>请参阅

[使用 CHeaderCtrl](../mfc/using-cheaderctrl.md)<br/>
[控件](../mfc/controls-mfc.md)
