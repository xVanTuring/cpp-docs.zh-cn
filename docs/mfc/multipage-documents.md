---
title: 多页文档
ms.date: 11/19/2018
helpviewer_keywords:
- pagination [MFC]
- overriding [MFC], View class functions for printing
- OnPrepareDC method [MFC]
- CPrintInfo structure [MFC], multipage documents
- OnEndPrinting method [MFC]
- protocols [MFC], printing protocol
- document pages vs. printer pages [MFC]
- printer mode [MFC]
- printing [MFC], multipage documents
- printers [MFC], printer mode
- documents [MFC], printing
- OnPreparePrinting method [MFC]
- OnPrint method [MFC]
- DoPreparePrinting method and pagination [MFC]
- OnDraw method [MFC], printing
- pagination [MFC], printing multipage documents
- printing [MFC], protocol
- pages [MFC], printing
- OnBeginPrinting method [MFC]
- multipage documents [MFC]
- printing [MFC], pagination
- documents [MFC], paginating
ms.assetid: 69626b86-73ac-4b74-b126-9955034835ef
ms.openlocfilehash: 81e03657977d31827c5c7c3d3272e3d4255a4a8b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62238463"
---
# <a name="multipage-documents"></a>多页文档

本文介绍 Windows 打印协议并说明如何打印包含多个页面的文档。 本文包含以下主题：

- [打印协议](#_core_the_printing_protocol)

- [重写视图类函数](#_core_overriding_view_class_functions)

- [分页](#_core_pagination)

- [打印机页与文档页](#_core_printer_pages_vs.._document_pages)

- [打印时分页](#_core_print.2d.time_pagination)

##  <a name="_core_the_printing_protocol"></a> 打印协议

为了打印多页文档，框架和视图将按以下方式交互。 首先，框架显示**打印**对话框中，创建设备上下文的打印机，并调用[StartDoc](../mfc/reference/cdc-class.md#startdoc)的成员函数[CDC](../mfc/reference/cdc-class.md)对象。 然后，对于文档的每一页，框架将调用[StartPage](../mfc/reference/cdc-class.md#startpage)成员函数`CDC`对象，指示视图对象打印该页，并调用[EndPage](../mfc/reference/cdc-class.md#endpage)成员函数。 如果启动特定页面之前，必须更改打印机模式，视图将调用[ResetDC](../mfc/reference/cdc-class.md#resetdc)，以便更新[DEVMODE](/windows/desktop/api/wingdi/ns-wingdi-_devicemodea)结构，它包含新打印机模式信息。 已打印整个文档，框架将调用[EndDoc](../mfc/reference/cdc-class.md#enddoc)成员函数。

##  <a name="_core_overriding_view_class_functions"></a> 重写视图类函数

[CView](../mfc/reference/cview-class.md)类定义多个成员函数，用于在打印期间由框架调用。 通过在视图类中重写这些函数，便能在框架的打印逻辑和您的视图类的打印逻辑之间建立连接。 下表列出了这些成员函数。

### <a name="cviews-overridable-functions-for-printing"></a>CView 的可重写的打印函数

|名称|重写的原因|
|----------|---------------------------|
|[OnPreparePrinting](../mfc/reference/cview-class.md#onprepareprinting)|在“打印”对话框中插入值，尤其是文档的长度|
|[OnBeginPrinting](../mfc/reference/cview-class.md#onbeginprinting)|分配字体或其他 GDI 资源|
|[OnPrepareDC](../mfc/reference/cview-class.md#onpreparedc)|为给定页调整设备上下文的特性，或执行打印时分页|
|[OnPrint](../mfc/reference/cview-class.md#onprint)|打印给定页|
|[OnEndPrinting](../mfc/reference/cview-class.md#onendprinting)|释放 GDI 资源|

您也可以在其他函数中执行与打印有关的处理，但这些函数是驱动打印过程的函数。

下图演示了打印过程涉及的步骤，并显示了 `CView` 的每个打印成员函数的调用位置。 本文的其余部分将更详细地说明大部分这些步骤。 打印过程的其他部分的文章中所述[分配 GDI 资源](../mfc/allocating-gdi-resources.md)。

![打印循环过程](../mfc/media/vc37c71.gif "打印循环过程") <br/>
打印循环

##  <a name="_core_pagination"></a> 分页

框架将存储中的打印作业有关的信息的大部分[CPrintInfo](../mfc/reference/cprintinfo-structure.md)结构。 `CPrintInfo` 中的某些值与分页有关；这些值是可访问的，如下表所示。

### <a name="page-number-information-stored-in-cprintinfo"></a>存储在 CPrintInfo 中的页码信息

|成员变量或<br /><br /> 函数名|引用的页码|
|-----------------------------------------------|----------------------------|
|`GetMinPage`/`SetMinPage`|文档的第一页|
|`GetMaxPage`/`SetMaxPage`|文档的最后一页|
|`GetFromPage`|要打印的第一页|
|`GetToPage`|要打印的最后一页|
|`m_nCurPage`|当前打印的页|

页码从 1 开始，即第一页的页码为 1，而不是 0。 有关这些和其他成员的详细信息[CPrintInfo](../mfc/reference/cprintinfo-structure.md)，请参阅*MFC 参考*。

在打印过程开始时，框架将调用该视图的[OnPreparePrinting](../mfc/reference/cview-class.md#onprepareprinting)成员函数，传递一个指向`CPrintInfo`结构。 应用程序向导提供的实现`OnPreparePrinting`的调用[DoPreparePrinting](../mfc/reference/cview-class.md#doprepareprinting)，另一个成员函数的`CView`。 `DoPreparePrinting` 是显示“打印”对话框并创建打印机设备上下文的函数。

此时，应用程序无法知道文档中有多少页。 它对文档的第一页和最后一页的页码使用默认值 1 和 0xFFFF。 如果您知道文档有多少页，重写`OnPreparePrinting`，并调用 [为 SetMaxPage]--brokenlink--(reference/cprintinfo-class.md#setmaxpage)`CPrintInfo`结构，在发送之前`DoPreparePrinting`。 这样，您便可以指定文档的长度。

`DoPreparePrinting` 随后显示“打印”对话框。 当它返回时，`CPrintInfo` 结构包含用户指定的值。 如果用户希望仅打印选定范围的页，他/她可以在“打印”对话框中指定开始和结束页码。 Framework 检索使用这些值`GetFromPage`并`GetToPage`的函数[CPrintInfo](../mfc/reference/cprintinfo-structure.md)。 如果用户未指定页范围，框架将调用 `GetMinPage` 和 `GetMaxPage` 并使用返回的值来打印整个文档。

对于要打印的文档的每个页，框架将调用两个成员函数在视图类中， [OnPrepareDC](../mfc/reference/cview-class.md#onpreparedc)并[OnPrint](../mfc/reference/cview-class.md#onprint)，并将每个函数传递两个参数： 一个指向[CDC](../mfc/reference/cdc-class.md)对象和一个指向`CPrintInfo`结构。 每次框架将调用`OnPrepareDC`并`OnPrint`，它将传递的值不同*m_nCurPage*的成员`CPrintInfo`结构。 这样，框架就能告知视图应该打印的页。

[OnPrepareDC](../mfc/reference/cview-class.md#onpreparedc)成员函数还用于屏幕显示。 它在绘制发生前对设备上下文进行调整。 `OnPrepareDC` 在打印中充当类似的角色，但有两个区别：首先，`CDC` 对象表示的是打印机设备上下文而不是屏幕设备上下文；其次，`CPrintInfo` 对象作为第二个参数传递。 (此参数是**NULL**时`OnPrepareDC`称为是用于屏幕显示。)重写 `OnPrepareDC` 以根据要打印的页调整设备上下文。 例如，您可以移动视区原点和剪辑区域以确保打印文档的相应部分。

[OnPrint](../mfc/reference/cview-class.md#onprint)成员函数执行页的实际打印。 文章[如何执行默认打印](../mfc/how-default-printing-is-done.md)演示了框架如何调用[OnDraw](../mfc/reference/cview-class.md#ondraw)使用打印机设备上下文以执行打印。 更准确地说，框架使用 `OnPrint` 结构和设备上下文调用 `CPrintInfo`，而 `OnPrint` 将设备上下文传递到 `OnDraw`。 重写 `OnPrint` 以执行只应在打印期间进行并且不是用于屏幕显示的任何渲染。 例如，若要打印页眉或页脚 (请参阅文章[页眉和页脚](../mfc/headers-and-footers.md)有关详细信息)。 然后，从 `OnDraw` 的重写调用 `OnPrint` 以执行屏幕显示和打印共用的渲染。

这一事实，`OnDraw`同时为屏幕显示和打印意味着应用程序的所见即所得执行渲染："所见即所得。" 但是，此处假定您没有编写所见即所得的应用程序。 例如，想象一下这样一个文本编辑器：使用粗体字体进行打印但显示控件代码以在屏幕上指示粗体文本。 在这种情况下，您应严格使用 `OnDraw` 进行屏幕显示。 当重写 `OnPrint` 时，请用对 `OnDraw` 的调用替换对单独的绘图函数的调用。 该函数将使用您不在屏幕上显示的特性，按照文档在纸上显示的方式绘制文档。

##  <a name="_core_printer_pages_vs.._document_pages"></a> 打印机页与文档页

提到页码，有时候必须区分打印机的页概念与文档的页概念。 从打印机的角度来看，一页就是一张纸。 但是，一张纸不一定等同于一页文档。 例如，如果打印的是要对折纸张的新闻稿，那么一张纸可能会并排放置文档的第一页和最后一页。 同样，如果打印的是电子表格，那么文档完全不包含页。 相反，一张纸可能包含 1 至 20 行，6 至 10 列。

统计中的所有页[CPrintInfo](../mfc/reference/cprintinfo-structure.md)结构是指打印机页。 框架将为要通过打印机的每张纸调用一次 `OnPrepareDC` 和 `OnPrint`。 当您重写[OnPreparePrinting](../mfc/reference/cview-class.md#onprepareprinting)函数以指定文档的长度，则必须使用打印机页。 如果存在一对一的对应关系（即一个打印机页等同于一个文档页），则此操作很容易。 另一方面，如果文档页和打印机页不直接对应，则必须对其进行相应的转换。 例如，考虑一下打印电子表格。 当重写 `OnPreparePrinting` 时，必须计算打印整个电子表需要多少张纸，然后在调用 `SetMaxPage` 的 `CPrintInfo` 成员函数时使用该值。 同样，重写时`OnPrepareDC`，则必须将转换*m_nCurPage*到范围中的行和列将显示在该特定工作表，然后相应地调整视区原点。

##  <a name="_core_print.2d.time_pagination"></a> 打印时分页

在某些情况下，视图类不能预先知道文档在实际打印前要等待多长时间。 例如，假定应用程序不是所见即所得的，那么文档在屏幕上的长度与其打印时的长度就不对应。

这会导致出现问题时您重写[OnPreparePrinting](../mfc/reference/cview-class.md#onprepareprinting)为视图类： 不能将传递到值`SetMaxPage`函数的[CPrintInfo](../mfc/reference/cprintinfo-structure.md)结构，因为您不知道的长度文档。 如果用户未“打印”对话框指定停止处的页码，框架就不知道何时停止打印循环。 确定何时停止打印循环的唯一方法是输出文档并查看它何时结束。 视图类必须在文档打印期间检查其末尾，然后告知框架何时到达末尾。

框架依赖视图类的[OnPrepareDC](../mfc/reference/cview-class.md#onpreparedc)函数以告知何时停止。 每次调用后`OnPrepareDC`，该框架将检查的成员`CPrintInfo`称为结构*m_bContinuePrinting*。 其默认值是 **，则返回 TRUE。** 只要此值保持为 TRUE，框架就会继续打印循环。 如果设置为**FALSE**，则框架将停止。 若要执行打印时分页，重写`OnPrepareDC`来检查是否已到达，并设置文档的结尾*m_bContinuePrinting*到**FALSE**它。

默认实现`OnPrepareDC`设置*m_bContinuePrinting*到**FALSE**如果当前页大于 1。 这意味着，如果未指定文档的长度，框架将假定文档的长度是一页。 这样的一个后果是，您在调用基类版本的 `OnPrepareDC` 时必须小心。 不要假定*m_bContinuePrinting*将为**TRUE**之后调用基类版本。

### <a name="what-do-you-want-to-know-more-about"></a>你想要了解更多信息

- [页眉和页脚](../mfc/headers-and-footers.md)

- [分配 GDI 资源](../mfc/allocating-gdi-resources.md)

## <a name="see-also"></a>请参阅

[打印](../mfc/printing.md)<br/>
[CView 类](../mfc/reference/cview-class.md)<br/>
[CDC 类](../mfc/reference/cdc-class.md)
