---
title: 源编辑器
description: 在 Visual Studio for Mac 中使用源编辑器
author: cobey
ms.author: cobey
ms.date: 05/06/2018
ms.assetid: A018A314-C1C4-4F36-BCB6-2D434208FCFE
ms.openlocfilehash: d1ea74b4893032252d04ebe5fe5e65ca1eedaeeb
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "68493245"
---
# <a name="source-editor"></a>源编辑器

可靠的源编辑器对简单高效地编写代码至关重要。 Visual Studio for Mac 提供了成熟的源编辑器，它是与 IDE 进行的交互的中心。 源编辑器提供了用户轻松工作所需的功能：从语法突出显示、代码片段和代码折叠等基础功能，到其 Roslyn 编译集成（如全功能 IntelliSense 代码完成）带来的优势，功能全面。

Visual Studio for Mac 中的源编辑器支持与 IDE 中的所有其他功能（如调试、重构和版本控制集成）的无缝体验。

本文介绍源编辑器的一些主要功能，并探讨如何使用 Visual Studio for Mac 来尽可能提高生产力。

## <a name="the-source-editor-experience"></a>源编辑器体验

快速查看代码并在其中高效移动是开发工作流的重要组成部分。 查看和维护代码的方式由自己确定，这可能因开发者而异，并且经常因项目而异。

Visual Studio for Mac 提供许多强大的功能，最大限度提高了跨平台开发的易用性和实用性。 以下部分介绍了一些重要功能。

## <a name="code-folding"></a>代码折叠

代码折叠支持开发者显示或隐藏完成的代码部分（如 using 指令、样板代码和注释以及 #region 语句），简化了大型源代码文件的管理。 在 Visual Studio for Mac 中，代码折叠默认为关闭状态

要打开代码折叠，请导航到“Visual Studio”>“首选项”>“文本编辑器”>“常规”>“代码折叠”  ：

![代码折叠选项](media/source-neweditor-image1.png)

此菜单还提供默认折叠 #regions 和注释、显示命名提示、替代代码的选项。

要显示或隐藏部分代码，请使用行号旁边的公开小组件：

![显示或隐藏部分代码](media/source-neweditor-image2.png)

也可通过使用“视图”>“折叠”>“切换折叠”/“切换所有折叠”菜单项，在显示和隐藏折叠间切换  ：

![折叠菜单项](media/source-editor-image19.png)

此菜单项也可用于启用或禁用代码折叠。

## <a name="word-wrap"></a>“自动换行”

当处理长代码行或视图空间有限时，自动换行可以帮助你管理空间。 自动换行还可以确保你的代码视图包含源文件的全部内容，即使在打开可能会遮挡视图或缩小源视图宽度的窗格时也是如此。 

自动换行默认禁用，但可以通过 Visual Studio for Mac 中的“首选项”启用  。 

要启用自动换行，请导航到“Visual Studio”>“首选项”>“文本编辑器”>“新编辑器”>“自动换行”  ：

![自动换行选项](media/source-neweditor-wordwrap1.png)

启用自动换行后，源文件中超出源编辑器视图宽度的行将自动换行到下一行。 还可以启用一个选项，以在换行的行旁边显示一个可见字形。 它可以帮助你区分已自动换行的行和已手动换行的行。

![启用了自动换行的已换行文本](media/source-neweditor-wordwrap2.png)

## <a name="ruler"></a>标尺

列标尺对于确定行长度很有帮助，对于具有行长度准则的工作团队尤其如此。 要打开或关闭列标尺，请导航到“Visual Studio”>“首选项”>“文本编辑器”>“标记和标尺”，并选中（或取消选中）“显示列标尺”，如下图中所示   ：

![首选项对话框，其中突出显示了“显示列标尺”](media/source-editor-image5.png)

 在源编辑器中，它显示为垂直的浅灰色直线。

## <a name="highlight-identifier-references"></a>突出显示标识符引用

启用“突出显示标识符引用”选项后，可以选择源代码中的任何符号，且源编辑器会向该文件中的所有其他引用提供一个直观的指南。 要启用此选项，请导航到“Visual Studio”>“首选项”>“文本编辑器”>“标记和标尺”，并选中“突出显示标识符引用”，如下图所示   ：

![首选项对话框，其中突出显示了“突出显示标识符引用”](media/source-editor-image6.png)

突出显示的颜色还有助于指示正在分配或引用的某些内容。 分配的内容以红色突出显示；引用的内容以蓝色突出显示：

![显示突出显示颜色的示例](media/source-editor-image7.png)

## <a name="see-also"></a>另请参阅

- [代码编辑器功能（Windows 上的 Visual Studio）](/visualstudio/ide/writing-code-in-the-code-and-text-editor)
- [大纲显示（Windows 上的 Visual Studio）](/visualstudio/ide/outlining)
