---
title: 如何：设置 IDE 辅助功能选项
description: 了解如何在 Visual Studio 中设置辅助功能选项，让每个人可以更轻松地使用其集成开发环境 (IDE) ，包括那些视力较差和写作能力有限的人。
ms.date: 08/22/2017
ms.topic: conceptual
helpviewer_keywords:
- accessibility [Visual Studio]
ms.assetid: ddc96c4c-0600-46c1-8267-7dce4c44ad24
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7a0b5835333bf8cd41ab653108054e2d3dd4c73e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919274"
---
# <a name="how-to-set-ide-accessibility-options"></a>如何：设置 IDE 辅助功能选项

> [!TIP]
> 若要详细了解最新的辅助功能更新，请参阅博文 [Visual Studio 2017 版本 15.3 中的辅助功能改进](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包含一些功能，可使有视觉障碍的人更方便地阅读，并使行动不便的人更方便地书写。 这些功能包括更改编辑器中文本的大小和颜色，更改工具栏上文本和按钮的大小，以及方法和参数的自动完成等。

此外，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持 Dvorak 键盘布局，这些布局使最频繁键入的字符使用起来更为方便。 还可以自定义适用于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的默认快捷键。 有关详细信息，请参阅[标识并自定义键盘快捷方式](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../environment-settings.md#reset-settings)。

## <a name="editors-dialogs-and-tool-windows"></a>编辑器、对话框和工具窗口

默认情况下，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中的对话框和工具窗口使用与操作系统相同的字号和颜色。 IDE 框架、对话框、工具栏和工具窗口的颜色设置是基于配色方案的：深色或浅色。 可在[“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)中更改当前颜色主题。

也可以在编辑器的“代码”视图中显示弹出窗口。 弹出窗口可以提示当前对象和参数的可用成员，以便完成函数或语句。 在键入有困难的情况下，这些窗口非常有用。 但是，它们会干扰代码编辑器中的焦点，这可能会对某些用户造成困扰。 通过打开“选项”对话框，并在“选项”对话框的“文本编辑器”->“所有语言”->“常规”页上清除“自动列出成员”和“参数信息”，可以关闭这些窗口       。

可以在集成开发环境 (IDE) 中重新排列窗口，以最适合的方式开展工作。 可以停靠、浮动、隐藏或自动隐藏每个工具窗口。

有关如何更改窗口布局的详细信息，请参阅[自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)。

### <a name="changing-the-size-of-text"></a>更改文本大小

可以在“工具”对话框中“环境”选项的“字体和颜色”窗格中更改基于文本的工具窗口的设置，例如“命令”窗口、“即时”窗口和“输出”窗口       。 在“显示其设置”下拉列表中选中“[全部文本工具窗口]”时，默认设置会在“项前景”和“项背景”下拉列表中作为“默认值”列出      。 还可以更改编辑器中文本显示方式的设置。

#### <a name="to-change-the-size-of-text-in-text-based-tool-windows-and-editors"></a>更改基于文本的工具窗口和编辑器中文本的大小

1. 从“工具”菜单中选择“选项”   。

2. 在“环境”文件夹上选择“字体和颜色”   。

3. 在“显示其设置”下拉菜单中选择一个选项  。

     若要更改编辑器中文本的字号，请选择“文本编辑器”  。

     若要更改基于文本的工具窗口中文本的字号，请选择“[全部文本工具窗口]”  。

     若要更改编辑器中工具提示文本的字号，请选择“编辑器工具提示”  。

     若要更改语句完成弹出消息中文本的字号，请选择“语句完成”  。

4. 从“显示项”中选择“纯文本”   。

5. 在“字体”中选择一个新的字体类型  。

6. 在“大小”中选择一个新的字号  。

    > [!NOTE]
    > 若要重置基于文本的工具窗口和编辑器的文本大小，请选择“使用默认值”  。

7. 选择 **“确定”** 。

### <a name="change-the-colors-that-are-used-in-the-ide"></a>更改 IDE 中使用的颜色

也可以选择更改编辑器中文本、边距指示器、空格和码位元素的默认颜色。

> [!NOTE]
> 若要对操作系统上的所有应用程序窗口使用高对比度的颜色，请按左 Alt+左 Shift+PrtScn  。 如果 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 处于打开状态，请关闭并重新打开 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以完全实现高对比度的颜色。

#### <a name="to-change-the-color-of-items-in-the-editor"></a>更改编辑器中项的颜色

1. 从“工具”菜单中选择“选项”   。

2. 在“环境”文件夹中选择“字体和颜色”   。

3. 在“显示其设置”中选择“文本编辑器”   。

4. 从“显示项”中选择要更改其显示方式的项，例如“纯文本”、“指示器边距”、“可见空白”、“HTML 特性名”或“XML 特性”       。

5. 从以下选项中选择显示设置：“项前景色”、“项背景色”和“粗体”    。

6. 选择 **“确定”** 。

## <a name="toolbars"></a>工具栏

为了提高工具栏的可用性和易用性，可以向工具栏按钮添加文本。

### <a name="to-assign-text-to-toolbar-buttons"></a>为工具栏按钮指定文本

1. 在“工具”菜单中选择“自定义”   。

2. 在“自定义”对话框中选择“命令”选项卡   。

3. 选择“工具栏”，然后选择包含要显示其文本的按钮的工具栏名称  。

4. 在列表中，选择要更改的命令。

5. 选择“修改所选内容”  。

6. 选择“图像和文本”  。

### <a name="to-modify-the-displayed-text-in-a-button"></a>修改按钮中的显示文本

1. 重新选择“修改所选内容”  。

2. 在“名称”旁边为选定的按钮插入一个新标题  。

## <a name="see-also"></a>请参阅

* [Visual Studio 的辅助功能](../../ide/reference/accessibility-features-of-visual-studio.md)
* [用于设计支持辅助功能的应用程序的资源](../../ide/reference/resources-for-designing-accessible-applications.md)