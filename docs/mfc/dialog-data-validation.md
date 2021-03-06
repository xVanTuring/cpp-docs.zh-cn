---
title: 对话框数据验证
ms.date: 11/04/2016
helpviewer_keywords:
- validating data [MFC], message boxes
- data validation [MFC], dialog boxes
- dialog boxes [MFC], validating data
- validating data [MFC], dialog box data entry
- DDV (dialog data validation) [MFC]
- data validation [MFC], message boxes
ms.assetid: f070c309-2044-4ff2-8c92-1ec1ea84af58
ms.openlocfilehash: cef9941cccd49ca61f0a93472636656f7241a61e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62383810"
---
# <a name="dialog-data-validation"></a>对话框数据验证

中的示例中所示，可以通过调用 DDV 函数指定除了数据交换的验证[对话框数据交换](../mfc/dialog-data-exchange.md)。 `DDV_MaxChars`在示例中调用验证文本框控件中输入的字符串不超过 20 个字符。 如果验证失败，并将焦点置于有问题的控件上，以便用户可以重新输入数据，DDV 函数通常向具有一个消息框的用户发出警报。 为同一个控件，必须 DDX 函数后立即调用给定控件的 DDV 函数。

此外可以定义自己的自定义 DDX 和 DDV 例程。 这和 DDX 和 DDV 的其他方面的详细信息，请参阅[MFC 技术说明 26](../mfc/tn026-ddx-and-ddv-routines.md)。

[添加成员变量向导](../ide/add-member-variable-wizard.md)编写所有 DDX 和 DDV 将为你的数据映射中调用。

## <a name="see-also"></a>请参阅

[对话框数据交换和验证](../mfc/dialog-data-exchange-and-validation.md)<br/>
[对话框的生命周期](../mfc/life-cycle-of-a-dialog-box.md)<br/>
[对话框数据交换](../mfc/dialog-data-exchange.md)
