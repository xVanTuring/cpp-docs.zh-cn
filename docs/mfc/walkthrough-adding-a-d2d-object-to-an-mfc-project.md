---
title: 演练：向 MFC 项目添加 D2D 对象
ms.date: 04/25/2019
helpviewer_keywords:
- MFC, D2D
- D2D [MFC]
ms.assetid: dda36c33-c231-4da6-a62f-72d69a12b6dd
ms.openlocfilehash: 5710add59c0e5d27b2969ae22087533cae901ca9
ms.sourcegitcommit: 283cb64fd7958a6b7fbf0cd8534de99ac8d408eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64558172"
---
# <a name="walkthrough-adding-a-d2d-object-to-an-mfc-project"></a>演练：向 MFC 项目添加 D2D 对象

本演练介绍了如何添加基本 Direct2D 到视觉对象 (D2D) 对象C++，Microsoft 基础类库 (MFC) 项目，然后生成项目的应用程序将打印为"Hello，world"渐变背景。

本演练演示如何完成这些任务：

- 创建 MFC 应用程序。

- 创建一个纯色画笔和线性渐变画笔。

- 修改渐变画笔，以便它将更改相应地调整窗口的大小。

- 实现 D2D 绘制处理程序。

- 验证结果。

[!INCLUDE[note_settings_general](../mfc/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>系统必备

若要完成本演练，必须具有 Visual Studio 一并安装**使用的桌面开发C++** 工作负荷和可选**VisualC++用于 x86 和 x64 的 MFC**组件。

## <a name="to-create-an-mfc-application"></a>若要创建的 MFC 应用程序

1. 使用**MFC 应用程序向导**创建 MFC 应用程序。 请参阅[演练：使用新的 MFC Shell 控件](walkthrough-using-the-new-mfc-shell-controls.md)有关如何打开你的 Visual Studio 版本的向导的说明。

1. 在中**名称**框中，键入*MFCD2DWalkthrough*。 选择 **“确定”**。

1. 在中**MFC 应用程序向导**，选择**完成**而无需更改任何设置。

## <a name="to-create-a-solid-color-brush-and-a-linear-gradient-brush"></a>若要创建一个纯色画笔和线性渐变画笔

1. 在中**解决方案资源管理器**，在**MFCD2DWalkthrough**项目，在**标头文件**文件夹中，打开 MFCD2DWalkthroughView.h。 添加到此代码`CMFCD2DWalkthroughView`类，以创建三个数据变量：

   ```cpp
   CD2DTextFormat* m_pTextFormat;
   CD2DSolidColorBrush* m_pBlackBrush;
   CD2DLinearGradientBrush* m_pLinearGradientBrush;
   ```

   保存该文件并将其关闭。

1. 在中**源文件**文件夹中，打开 MFCD2DWalkthroughView.cpp。 构造函数中`CMFCD2DWalkthroughView`类中，添加此代码：

   ```cpp
   // Enable D2D support for this window:
   EnableD2DSupport();

   // Initialize D2D resources:
   m_pBlackBrush = new CD2DSolidColorBrush(
       GetRenderTarget(),
       D2D1::ColorF(D2D1::ColorF::Black));

   m_pTextFormat = new CD2DTextFormat(
       GetRenderTarget(),
       _T("Verdana"),
       50);

   m_pTextFormat->Get()->SetTextAlignment(
       DWRITE_TEXT_ALIGNMENT_CENTER);

   m_pTextFormat->Get()->SetParagraphAlignment(
       DWRITE_PARAGRAPH_ALIGNMENT_CENTER);

   D2D1_GRADIENT_STOP gradientStops[2];

   gradientStops[0].color =
       D2D1::ColorF(D2D1::ColorF::White);

   gradientStops[0].position = 0.f;
   gradientStops[1].color =
       D2D1::ColorF(D2D1::ColorF::Indigo);

   gradientStops[1].position = 1.f;

   m_pLinearGradientBrush = new CD2DLinearGradientBrush(
       GetRenderTarget(),
       gradientStops,
       ARRAYSIZE(gradientStops),
       D2D1::LinearGradientBrushProperties(
           D2D1::Point2F(0,0),
           D2D1::Point2F(0,0)));
   ```

   保存该文件并将其关闭。

## <a name="to-modify-the-gradient-brush-so-that-it-will-change-appropriately-when-the-window-is-resized"></a>若要修改渐变画笔，以便它将更改相应地调整窗口的大小

1. 上**项目**菜单中，选择**类向导**。

1. 在中**MFC 类向导**下**类名**，选择`CMFCD2DWalkthroughView`。

1. 上**消息**选项卡上，在**消息**框中，选择`WM_SIZE`，然后选择**添加处理程序**。 此操作将添加`OnSize`消息处理程序到`CMFCD2DWalkthroughView`类。

1. 在中**现有的处理程序**框中，选择`OnSize`。 选择**编辑代码**以显示`CMFCD2DWalkthroughView::OnSize`方法。 在该方法的末尾，添加以下代码。

   ```cpp
   m_pLinearGradientBrush->SetEndPoint(CPoint(cx, cy));
   ```

   保存该文件并将其关闭。

## <a name="to-implement-a-d2d-drawing-handler"></a>若要实现 D2D 绘制处理程序

1. 上**项目**菜单中，选择**类向导**。

1. 在中**MFC 类向导**下**类名**，选择`CMFCD2DWalkthroughView`。

1. 上**消息**选项卡上，选择**添加自定义消息**。

1. 在中**添加自定义消息**对话框中**自定义 Windows 消息**框中，键入*AFX_WM_DRAW2D*。 在中**消息处理程序名称**框中，键入*OnDraw2D*。 选择**注册消息**选项，然后选择**确定**。 此操作将添加到 AFX_WM_DRAW2D 消息的消息处理程序`CMFCD2DWalkthroughView`类。

1. 在中**现有的处理程序**框中，选择`OnDraw2D`。 选择**编辑代码**以显示`CMFCD2DWalkthroughView::OnDraw2D`方法。 使用此代码`CMFCD2DWalkthroughView::OnDrawD2D`方法：

   ```cpp
   afx_msg LRESULT CMFCD2DWalkthroughView::OnDraw2D(
       WPARAM wParam,
       LPARAM lParam)
   {
       CHwndRenderTarget* pRenderTarget = (CHwndRenderTarget*)lParam;
       ASSERT_VALID(pRenderTarget);

       CRect rect;
       GetClientRect(rect);

       pRenderTarget->FillRectangle(rect, m_pLinearGradientBrush);

       pRenderTarget->DrawText(
           _T("Hello, World!"),
           rect,
           m_pBlackBrush,
           m_pTextFormat);

       return TRUE;
   }
   ```

   保存该文件并将其关闭。

## <a name="to-verify-the-results"></a>若要验证结果

生成并运行应用程序。 它应具有时调整窗口的大小将更改一个梯度矩形。 "Hello World ！" 应显示在矩形的中心。

## <a name="see-also"></a>请参阅

[演练](../mfc/walkthroughs-mfc.md)
