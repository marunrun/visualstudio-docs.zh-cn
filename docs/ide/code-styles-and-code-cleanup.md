---
title: 代码样式选项和代码清理
ms.date: 04/25/2019
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Code_Style.General
- VS.ToolsOptionsPages.Text_Editor.Basic.Code_Style.General
ms.workload:
- multiple
ms.openlocfilehash: 4c7bb8f3e94a761023a19a5ea3361073b73d9f3b
ms.sourcegitcommit: 90c3187d804ad7544367829d07ed4b47d3f8a72d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68822425"
---
# <a name="code-style-preferences"></a>代码样式首选项

可以使用 [EditorConfig 文件](#code-styles-in-editorconfig-files)为每个项目定义代码样式设置，也可以在文本编辑器[选项](#code-styles-in-the-options-dialog-box)页面上为在 Visual Studio 中编辑的所有代码定义代码样式设置  。 对于 C# 代码，还可以使用“代码清理”（Visual Studio 2019）和“设置文档格式”（Visual Studio 2017）命令将 Visual Studio 配置为应用这些代码样式首选项   。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中的编辑器行为](/visualstudio/mac/editor-behavior)。

## <a name="code-styles-in-editorconfig-files"></a>EditorConfig 文件中的代码样式

通过将 [EditorConfig](create-portable-custom-editor-options.md) 文件添加到项目，可以指定 .NET 的[代码样式设置](../ide/editorconfig-code-style-settings-reference.md)。 EditorConfig 文件与基本代码（而不是 Visual Studio 个性化帐户）相关联。 EditorConfig 文件中的设置优先于“选项”对话框中指定的代码样式  。 如果想要将所有参与者的编码样式强制执行到存储库或项目，请使用 EditorConfig 文件。

::: moniker range=">=vs-2019"

可以手动填充 EditorConfig 文件，也可以根据已在 Visual Studio“选项”对话框中选择的代码样式设置自动生成文件  。 此选项页面位于“工具” > “选项” > “文本编辑器”>“[C# 或 Basic]”>“代码样式” > “常规”        。 单击“通过设置生成 .editorconfig 文件”，基于此“选项”页上的设置来自动生成编码样式 .editorconfig 文件    。

![通过 Visual Studio 2019 中的设置生成 editorconfig 文件](media/vs-2019/generate-editorconfig-file-small.png)

::: moniker-end

## <a name="code-styles-in-the-options-dialog-box"></a>“选项”对话框中的代码样式

打开“工具”菜单中的“选项”对话框，即可设置所有 C# 和 Visual Basic 项目的代码样式首选项   。 在“选项”对话框中，选择“文本编辑器”>“[C# 或 Basic]”>“代码样式” > “常规”       。

列表中的每一项都会显示所选首选项的预览：

::: moniker range="vs-2017"

![代码样式选项](media/code-style-quick-actions-dialog.png)

::: moniker-end

::: moniker range=">=vs-2019"

![代码样式选项](media/vs-2019/code-style-quick-actions-dialog.png)

::: moniker-end

在此窗口中设置的选项适用于 Visual Studio 个性化帐户，并且不与特定项目或基本代码相关联。 此外，它们不会在生成时（包括在持续集成 (CI) 生成中）强制执行。 如果要将代码样式首选项与项目关联，并在生成期间强制执行样式，请在与该文件关联的 [.editorconfig 文件](#code-styles-in-editorconfig-files)中指定首选项。

### <a name="preference-and-severity"></a>首选项和严重级别

对于此页上的每个样式设置，可使用每行相应的下拉列表设置“首选项”  和“严重性”  值。 严重性可设置为“仅重构”  、“建议”  、“警告”  或“错误”  。 如果想要为某个代码样式启用[快速操作](../ide/quick-actions.md)，请确保“严重性”  设置为“仅重构”  以外的其他项。 “快速操作”灯泡![灯泡](media/light-bulb-dropdown.png)、错误灯泡![错误灯泡](media/error-bulb.png)或螺丝刀![螺丝刀](media/screwdriver.png)图标将在使用了非首选样式时出现，你可选择“快速操作”列表上的选项将代码自动重写为首选样式   。

## <a name="apply-code-styles"></a>应用代码样式

::: moniker range="vs-2017"

可以配置“设置文档格式”命令（“编辑” > “高级” > “设置文档格式”）以应用代码样式设置（来自 EditorConfig 文件或“代码样式”选项）及其执行的常规设置格式（如缩进）      。 如果项目存在 .editorconfig 文件，则优先采用这些设置  。

> [!NOTE]
> 使用“设置文档格式”命令应用代码样式仅适用于 C# 代码文件  。 这是一项实验性功能。

配置希望“设置文档格式”在[“设置文档格式”选项页](reference/options-text-editor-csharp-formatting.md#format-document-settings)上应用的设置  。

![Visual Studio 2017 中格式文档的代码样式设置](media/format-document-settings-experiment.png)

> [!TIP]
> 严重性配置为“无”的规则不参与代码清理，但可通过“快速操作和重构”菜单单独应用   。

首次触发“设置文档格式”命令时，将显示一个黄色信息栏，提示你配置代码清理设置  。

::: moniker-end

::: moniker range=">=vs-2019"

对于 C# 代码文件，Visual Studio 2019 在编辑器底部有一个“代码清理”按钮  （键盘：“Ctrl”+“K”、“Ctrl”+“E”），可通过此按钮从 EditorConfig 文件或从“代码样式”选项页应用代码样式      。 如果项目存在 .editorconfig 文件，则优先采用这些设置  。

![在 Visual Studio 2019 中执行代码清理](media/execute-code-cleanup.png)

> [!TIP]
> 严重性配置为“无”的规则不参与代码清理，但可通过“快速操作和重构”菜单单独应用   。

首先，在“配置代码清理”对话框中配置要应用的代码样式（在两个配置文件中的某个文件中）  。 要打开此对话框，请单击代码清理扫帚图标旁边的展开箭头，然后选择“配置代码清理”  。

![在 Visual Studio 2019 中配置代码清理](media/configure-code-cleanup.png)

配置代码清理后，可以单击扫把图标，或者按“Ctrl+K，Ctrl+E”，来运行代码清理。     此外，还可以在整个项目或解决方中运行代码清理功能。 在“解决方案资源管理器”中右键单击项目或解决方案名称，选择“分析和代码清理”，然后选择“运行代码清理”。   

![在整个项目或解决方中运行代码清理功能](media/run-code-cleanup-project-solution.png)

如果希望每次保存文件时都应用代码样式设置，则可能需要使用[保存时清理代码](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.CodeCleanupOnSave)扩展。

::: moniker-end

## <a name="see-also"></a>请参阅

- [快速操作](../ide/quick-actions.md)
- [EditorConfig 的 .NET 编码约定设置](../ide/editorconfig-code-style-settings-reference.md)
- [编辑器行为 (Visual Studio for Mac)](/visualstudio/mac/editor-behavior)
