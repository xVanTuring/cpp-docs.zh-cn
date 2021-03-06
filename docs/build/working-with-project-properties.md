---
title: 设置C++在 Visual Studio 中的编译器和生成属性
description: 使用 Visual Studio IDE 来更改C++编译器和链接器选项和其他生成设置。
ms.date: 03/27/2019
helpviewer_keywords:
- project properties [C++], modifying
- properties [C++]
- Visual C++ projects, properties
- projects [C++], properties
ms.assetid: 9b0d6f8b-7d4e-4e61-aa75-7d14944816cd
ms.openlocfilehash: a8c15de43a3843b8ff12cb4ad3d951d76b90c039
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65446192"
---
# <a name="set-compiler-and-build-properties"></a>设置编译器和生成属性

在 IDE 中，生成项目的需要的全部信息都公开为属性。 此信息包括应用程序名称、扩展名（如 DLL、LIB、EXE）、编译器选项、链接器选项、调试器设置、自定义生成步骤和许多其他操作。 通常情况下，使用属性页（“项目”&#124;“属性”）来查看和修改这些属性。 若要访问的属性页，选择**项目 >\<项目名称 > 属性**从主菜单中或右键单击项目节点中**解决方案资源管理器**，然后选择**属性**。

## <a name="default-properties"></a>默认属性

创建项目时，系统分配各种属性的值。 根据项目类型和在应用向导中所选的选项类型，默认值会有所不同。 例如，ATL 项目具有与 MIDL 文件相关的属性，但这些属性在基本控制台应用程序中都不存在。 默认属性在属性页的“常规”窗格中显示：

![Visual C&#43; &#43;项目默认值](media/visual-c---project-defaults.png "VisualC++项目默认值")

## <a name="applying-properties-to-build-configurations-and-target-platforms"></a>将属性的配置和目标平台生成应用

某些属性（例如应用程序名称）适用于所有生成变量，而不考虑目标平台或其为调试版本还是发布版本。 但是大多数属性都依赖于配置。 这是由于编译器必须知道程序将在哪个特定平台上运行，以及使用哪个特定编译器选项以便生成正确的代码。 因此，设置属性时，请务必注意新值应适用于哪个配置和平台。 它应该仅适用于调试 Win32 版本还是也适用于调试 ARM 和调试 x64 版本？ 例如，默认情况下，“优化”属性在版本配置中设为“最大化速度(/O2)”，但在调试配置中禁用。

这样设置属性页是便于随时可以查看并在必要时修改属性值应适用于哪个配置和平台。 下图显示了属性页，该页的顶部列表框中包含配置和平台信息。 在此处设置“优化”属性时，它将仅适用于调试 Win32 版本，这正好是活动配置，如红色箭头所示。

![显示活动配置的 Visual C&#43;&#43;属性页](media/visual-c---property-pages-showing-active-configuration.png "显示活动配置的 Visual C++ 属性页")

下图显示相同的项目属性页，但该配置已更改为发布。 请注意“优化”属性的不同值。 另请注意，活动配置仍是调试。 可以在此处设置任何配置的属性；它不必处于活动状态。

![显示版本配置的 Visual C&#43;&#43; 属性页](media/visual-c---property-pages-showing-release-config.png "显示版本配置的 Visual C++ 属性页")

## <a name="target-platforms"></a>目标平台

目标平台是指可执行文件将在此之上运行的各种设备和/或操作系统。 可以生成多个平台的项目。 C++ 项目的可用目标平台取决于各种项目；包括但不限于 Win32、x64、ARM、Android 和 iOS。     可能在 Configuration Manager 中看到的 x86 目标平台等同于本机 C++ 项目中的 Win32。 Win32 意味着 32 位的 Windows，而 x64 意味着 64 位的 Windows。 有关这两个平台的详细信息，请参阅[运行 32 位的应用程序](/windows/desktop/WinProg64/running-32-bit-applications)。

可能在 Configuration Manager 中看到的任意 CPU 目标平台值对本机 C++ 项目无影响；而是与 C++/CLI 和其他 .NET 项目类型相关。 有关详细信息，请参阅 [/CLRIMAGETYPE（指定 CLR 映像的类型）](reference/clrimagetype-specify-type-of-clr-image.md)。


有关设置属性的调试版本的详细信息，请参阅：

- [C++ 调试配置的项目设置](/visualstudio/debugger/project-settings-for-a-cpp-debug-configuration)
- [调试器设置和准备](/visualstudio/debugger/debugger-settings-and-preparation)
- [调试准备：VisualC++项目类型](/visualstudio/debugger/debugging-preparation-visual-cpp-project-types)
- [在 Visual Studio 调试器中指定符号 (.pdb) 和源文件](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)

## <a name="c-compiler-and-linker-options"></a>C++编译器和链接器选项

C++编译器和链接器选项位于**C /C++** 并**链接器**下的左窗格中的节点**配置属性**。 将上述内容转换直接向将传递给编译器的命令行选项。 若要阅读有关特定选项的文档，该选项中选择中心窗格中，按**F1**。 或者，您可以浏览所有选项的文档[MSVC 编译器选项](reference/compiler-options.md)并[MSVC 链接器选项](reference/linker-options.md)。 

**属性页**对话框将显示与当前项目相关的属性页。 例如，如果该项目没有 .idl 文件则不会显示 MIDL 属性页。 在每个属性页上设置的详细信息，请参阅[属性页 (C++)](reference/property-pages-visual-cpp.md)。 

## <a name="directory-and-path-values"></a>目录和路径值

MSBuild 支持使用称为"宏"某些字符串值包括目录和路径的编译时常量。 它们在属性页中，可以在此引用，并使用修改[属性编辑器](#property_editor)。 

下图显示的属性页的 Visual StudioC++项目。 在左窗格中，选中“VC++ 目录”规则，右窗格中即会列出与该规则关联的属性。 `$(...)`值称为*宏*。 宏是编译时常量，是指由 Visual Studio 或 MSBuild 系统定义的值，或是由用户定义的值。 通过而不硬编码值，例如目录路径中使用宏，可以更轻松地共享计算机之间和 Visual Studio 版本之间的属性设置，可以更好地确保项目设置中正确地参与[属性继承](project-property-inheritance.md)。 

![项目属性页](media/project_property_pages_vc.png "Project_Property_Pages_VC")

可以使用属性编辑器来查看所有可用宏的值。

### <a name="predefined-macros"></a>预定义宏

全局宏<br/>
应用于项目配置的所有项目。 具有语法 `$(name)`。 全局宏的示例是 `$(VCInstallDir)`，它存储 Visual Studio 安装的根目录。 全局宏与 MSBuild 中的 `PropertyGroup` 相对应。

项宏<br/>
具有语法 `%(name)`。 对于文件来说，仅适用于该文件的项宏，例如可以使用 `%(AdditionalIncludeDirectories)` 来指定仅适用于特定文件的包含目录。 这种项宏与 MSBuild 中的 `ItemGroup` 元数据相对应。 在项目配置中使用时，项宏适用于特定类型的所有文件。 例如，C/C++“预处理器定义”配置属性可以采用适用于项目中所有 .cpp 文件的 `%(PreprocessorDefinitions)` 项宏。 这种项宏与 MSBuild 中的 `ItemDefinitionGroup` 元数据相对应。 有关详细信息，请参阅[项定义](/visualstudio/msbuild/item-definitions)。

### <a name="user-defined-macros"></a>用户定义的宏

你可以创建用户定义的宏，以便在项目生成中将宏用作变量。 例如，可以创建一个用户定义的宏来提供自定义生成步骤或自定义生成工具的值。 用户定义的宏是名称/值对。 在项目文件中，使用 $(<em>name</em>) 表示法访问该值。

用户定义的宏存储在属性表中。 如果你的项目尚未包含属性表，则可以创建一个下的步骤[共享或重用 Visual Studio 项目设置](create-reusable-property-configurations.md)。

#### <a name="to-create-a-user-defined-macro"></a>创建用户定义的宏

1. 在“属性管理器”窗口中（在菜单栏上，依次选择“视图”、“属性管理器”），打开属性表的快捷菜单（名称以 .user 结尾），然后选择“属性”。 此时将打开该属性表的“属性页”对话框。

1. 在对话框的左窗格中，选择“用户宏”。 在右窗格中，选择“添加宏”按钮，打开“添加用户宏”对话框。

1. 在对话框中，指定宏的名称和值。 根据需要，选中“将此宏设置为生成环境中的环境变量”复选框。

## <a name="property_editor">属性编辑器</a>

你可以使用属性编辑器来修改特定字符串属性，选择宏作为值。 若要访问“属性编辑器”，在属性页中选择属性，然后选择右侧的向下箭头按钮。 如果下拉列表包含“\<编辑>”，那么你可以选择它来显示该属性的属性编辑器。

![属性&#95;编辑器&#95;下拉列表](media/property_editor_dropdown.png "Property_Editor_Dropdown")

在属性编辑器中，可以选择“宏”按钮查看可用宏及这些宏的当前值。 下图显示选中“宏”按钮后，“附加包含目录”属性的属性编辑器。 如果选中“从父级或项目默认设置继承”复选框并添加了新值，则该值会附加到当前被继承的任意值。 如果清除复选框，则新值会替换继承值。 在大多数情况下，选中复选框。

![属性编辑器，Visual C&#43;&#43;](media/propertyeditorvc.png "PropertyEditorVC")

## <a name="add-an-include-directory-to-the-set-of-default-directories"></a>将包含目录添加到默认目录集

在将包含目录添加到项目中时，请勿重写所有默认目录，这点非常重要。 添加目录的正确方法是追加新路径，例如"C:\MyNewIncludeDir\\"，然后追加“$(IncludePath)”宏为属性值。

## <a name="quickly-browse-and-search-all-properties"></a>快速浏览和搜索所有属性

“所有选项”属性页（在“属性页”对话框中“配置属性”&#124;“C/C++”节点下）可实现快速浏览和搜索当前上下文中可用的属性。 它具有特殊的搜索框和简单的语法，能够帮助你筛选结果：

无前缀：<br/>
仅在属性名称中搜索（不区分大小写的子字符串）。

'/' 或 '-'：<br/>
仅在编译器开关中搜索（不区分大小写的前缀）

v:<br/>
仅在值中搜索（不区分大小写的子字符串）。

## <a name="set-environment-variables-for-a-build"></a>为生成设置环境变量

MSVC 编译器 (cl.exe) 可识别某些环境变量，专门 LIB、 LIBPATH、 PATH 和 INCLUDE。 使用 IDE 生成时，[VC++ Directories Property Page](reference/vcpp-directories-property-page.md) 属性页中设置的属性用于设置那些环境变量。 如果已设置了 LIB、LIBPATH 和 INCLUDE 值（例如通过开发人员命令提示设置），则这些值将被相应的 MSBuild 属性的值替换。 然后生成在 PATH 前预置 VC++ 目录可执行目录属性的值。 你可以通过创建用户定义的宏然后选中显示“在生成环境中将此宏设置为环境变量”的框来设置用户定义的环境变量。

## <a name="set-environment-variables-for-a-debugging-session"></a>为调试会话设置环境变量

在项目“属性页”对话框的左窗格中，展开“配置属性”，然后选择“调试”。

在右窗格中，修改“环境”或“合并环境”项目设置，然后选择“确定”按钮。

## <a name="in-this-section"></a>本节内容

[共享或重用 Visual Studio 项目设置](create-reusable-property-configurations.md)<br/>
如何创建具有可共享的自定义生成设置或 resused.props 文件。

[项目属性继承](project-property-inheritance.md)<br/>
介绍.props、.targets、.vcxproj 文件和生成过程中的环境变量的评估顺序。

[在不更改项目文件的情况下修改属性和目标](modify-project-properties-without-changing-project-file.md)<br/>
如何创建临时生成设置，而无需修改项目文件。 

## <a name="see-also"></a>请参阅

[Visual Studio 项目 - C++](creating-and-managing-visual-cpp-projects.md)<br/>
[.vcxproj 和 .props 文件结构](reference/vcxproj-file-structure.md)<br/>
[属性页 XML 文件](reference/property-page-xml-files.md)<br/>
