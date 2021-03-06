---
title: 在 Rich Edit 控件中打印
ms.date: 11/04/2016
helpviewer_keywords:
- printing [MFC], CRichEditCtrl
- rich edit controls [MFC], printing
- CRichEditCtrl class [MFC], printing
ms.assetid: dbda0e40-018f-424e-b5d8-7b489aaf27af
ms.openlocfilehash: 2ddc52e43da2e409117ccc5169442002ac27a315
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62238390"
---
# <a name="printing-in-rich-edit-controls"></a>在 Rich Edit 控件中打印

您可以告诉 rich edit 控件 ([CRichEditCtrl](../mfc/reference/cricheditctrl-class.md)) 来呈现指定的设备，例如打印机其输出。 此外可以指定为其 rich edit 控件的输出设备设置其文本的格式。

若要设置格式的特定设备的 rich edit 控件内容的一部分，可以使用[FormatRange](../mfc/reference/cricheditctrl-class.md#formatrange)成员函数。 [FORMATRANGE](/windows/desktop/api/richedit/ns-richedit-_formatrange)结构与此函数使用指定的目标设备的设备上下文 (DC) 以及设置格式的文本范围。

在设置格式文本的输出设备之后, 您可以将输出发送到设备使用[DisplayBand](../mfc/reference/cricheditctrl-class.md#displayband)成员函数。 通过重复使用`FormatRange`和`DisplayBand`，打印格式文本编辑控件的内容应用程序可以实现条带。 （条带是输出划分为若干较小部分供打印。）

可以使用[SetTargetDevice](../mfc/reference/cricheditctrl-class.md#settargetdevice)成员函数来指定为其 rich edit 控件的目标设备设置其文本的格式。 此函数可用于所见即所得 （所见即所得） 格式设置，在其中的应用程序定位使用默认打印机的字体规格而不屏幕的文本。

## <a name="see-also"></a>请参阅

[使用 CRichEditCtrl](../mfc/using-cricheditctrl.md)<br/>
[控件](../mfc/controls-mfc.md)
