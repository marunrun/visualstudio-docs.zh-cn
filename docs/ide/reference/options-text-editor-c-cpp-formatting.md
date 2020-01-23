---
title: 选项，文本编辑器，C/C++，格式
ms.date: 04/30/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.C%2fC%2b%2b.Formatting.General
dev_langs:
- CPP
helpviewer_keywords:
- Text Editor Options dialog box, formatting
- ClangFormat
ms.assetid: cb6f1cbb-5305-48da-a8e8-33fd70775d46
author: TerryGLee
ms.author: tglee
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: d7a6029058ab0bc02a623df0e1733eb8548102d5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596250"
---
# <a name="options-text-editor-cc-formatting"></a>选项，文本编辑器，C/C++，格式

使用 C 或 C++ 进行编程时，请使用以下属性页更改代码编辑器的默认行为。

![C++ Formatting 属性页](media/cpp-formatting.png)

若要访问此页，请在“选项”  对话框的左窗格中，展开“文本编辑器”  ，再展开“C/C++”  ，然后单击“格式设置”  。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)。

## <a name="general-page"></a>常规页

此页面有一些选项，可用于在键入语句和块时设置其格式。

::: moniker range="vs-2017"

**Visual Studio 2017 版本 15.7 及更高版本**：

::: moniker-end

此页面还包含用于配置 [ClangFormat](https://clang.llvm.org/docs/ClangFormat.html) 版本 5.0 支持的选项。 ClangFormat 是一款实用工具，能够根据 .clang-format 或 _clang-format 文件中可配置的一组规则轻松设置代码样式和格式。

### <a name="configuring-clangformat-options"></a>配置 ClangFormat 选项

::: moniker range="vs-2017"

**Visual Studio 2017 版本 15.7 及更高版本**：

::: moniker-end

默认情况下，启用 ClangFormat 支持。 可选择对所有项目应用下述一种常见的格式约定：LLVM、Google、Chromium、Mozilla 或 Webkit。 此外，还可创建自定义格式定义 .clang-format 或 _clang-format 文件。 如果项目文件夹中存在此类文件，Visual Studio 将使用它来设置该文件夹及其子文件夹中所有源代码文件的格式。

当你键入内容时，Visual Studio 默认在背景应用格式中运行 clangformat.exe。 此外，还可指定仅针对“设置文档格式(Ctrl+K, Ctrl+D)”或“设置选定内容格式(Ctrl+K, Ctrl+F)”这两个手动调用的格式命令运行它   。

## <a name="indentation-new-lines-spacing-wrapping-pages"></a>“缩进”、“新行”和“间距换行”页面

这些页面支持各种格式自定义；但如果启用了 ClangFormat，则忽略这些页面。

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
- [使用 IntelliSense](../../ide/using-intellisense.md)
