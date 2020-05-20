---
title: 全屏和虚拟空间模式
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- word wrap
- views, virtual space
- line numbers, displaying
- virtual space mode
- line numbers
- Code Editor, view and display options
- full screen mode
- Code Editor, modes
- views, splitting
- views, word wrapping
- fonts and size
- views, creating new windows
- views, line numbers
- views, changing mode
- views, outlining
ms.assetid: 1fb48027-d870-439f-8b72-4a0321390748
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 77f224a6e3a1b12ed17799ddf6a2fc5c23f5d4cc
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75591029"
---
# <a name="how-to-manage-editor-modes"></a>如何：管理编辑器模式

可在各种显示模式下显示 Visual Studio 代码编辑器。

> [!NOTE]
> 显示的对话框和菜单命令可能与本文中的描述不同，具体取决于现用的设置或版本。 若要更改设置，例如“常规”或“Visual C++”设置，请选择“工具” > “导入和导出设置”，再选择“重置所有设置”。

## <a name="enable-full-screen-mode"></a>启用全屏模式

启用“全屏”模式后，可选择隐藏所有工具窗口并仅查看文档窗口  。

- 按 **Alt**+**Shift**+**Enter** 可进入或退出“全屏”  模式。

     --或者--

- 在“命令”窗口中发出命令 `View.Fullscreen`  。

## <a name="enable-virtual-space-mode"></a>启用虚空格模式

在“虚空格”模式下，将在每个代码行末尾插入空格  。 选择此选项可将注释放置在代码旁的一致位置。

1. 从“工具”菜单中选择“选项”   。

2. 展开“文本编辑器”文件夹，选择“所有语言”，全局设置此选项，或选择特定语言的文件夹   。 例如，若要仅在 Visual Basic 中启用行号，则选择“Basic” > “文本编辑器”节点。

3. 选择“常规”选项，然后在“设置”下选择“启用虚空格”    。

    > [!NOTE]
    > “虚空格”在“列选择”模式下启用   。 如果未启用“虚空格”模式，插入点将从一行的末尾直接移动到下一行的第一个字符  。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)
- [“选项”对话框 ->“环境”->“字体和颜色”](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)
