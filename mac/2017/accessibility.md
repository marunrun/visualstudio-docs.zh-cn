---
title: 可访问性
description: 本文介绍 Visual Studio for Mac 中的辅助功能及其启用方法。
author: conceptdev
ms.author: crdun
ms.date: 08/15/2017
ms.assetid: 2C4AAC2E-3B4A-4496-8BE0-1F5A7F81D1CA
ms.openlocfilehash: f90f5fca9d68ed00162fd746ddf291343c8d51f7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62988384"
---
# <a name="accessibility"></a>可访问性

除了 macOS 中的功能和实用工具，Visual Studio for Mac 还提供下列功能，旨在更方便残障人士使用：

- Solution Pad 和 Editor Pad 中的文本放大选项
- 编辑器中的文本大小选项
- 编辑器中的颜色自定义
- 键盘快捷方式自定义
- 支持对方法和参数使用代码完成功能

若要详细了解 macOS 中的辅助功能，请访问 [Apple 网站](https://www.apple.com/accessibility/mac/)。

## <a name="using-accessibility-features-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中使用辅助功能

Visual Studio for Mac 中的辅助功能默认处于禁用状态。 若要启用辅助功能，请按照下列步骤操作：

1. 依次转到“Visual Studio”>“首选项”>“其他”>“辅助功能”。

2. 选中“启用辅助功能”复选框，如下图所示：

    ![“启用辅助功能”复选框](media/accessibility-image1.png)

3. 按“重启 Visual Studio”按钮，以启用辅助功能。

也可以使用命令行启用辅助功能。 为此，请在终端中输入以下命令：

```bash
defaults write com.microsoft.visual-studio com.monodevelop.AccessibilityEnabled 1
```

启用辅助功能后，需要重启 Visual Studio。

## <a name="how-to-use-keyboard-navigation"></a>如何：使用键盘导航

可以依次转到“系统首选项”>“键盘”>“快捷方式”，将“完全键盘访问权限”选项设置为“所有控件”，从而启用键盘导航：

![macos 中的“系统首选项”面板](media/accessibility-image2.png)

设置完全键盘访问权限会启用聚焦框。 然后，可以使用下列方法之一选择控件：

- 按 Tab 前移切换控件
- 按 Shift-Tab 后移切换控件
- 按箭头键沿箭头方向切换控件。

按空格键激活焦点所在的控件。

## <a name="how-to-enable-and-use-voice-over"></a>如何：启用和使用 Voice Over

按 Cmd + F5 启用或禁用 VoiceOver

若要切换 UI VoiceOver 命令，请使用以下命令：

- 在控件之间移动 VoiceOver 游标：Ctrl + Alt + 向左键/向右键

   VoiceOver 会读出控件名称、一些相关详情和具体用法。

- 进入组和控件（如 Solution Pad、Toolbox 和其他 Pad）：Ctrl + Alt + Shift + 向下键

   进入控件后，可以使用 Ctrl + Alt + 箭头键在控件内部移动。

有关如何使用 macOS 中的 VoiceOver 的常规信息，请参阅以下指南：

- [VoiceOver 入门](https://help.apple.com/voiceover/info/guide/10.12/)
- [macOS 中的 VoiceOver 命令](http://lab.dotjay.com/notes/voiceover-commands/)

## <a name="see-also"></a>请参阅

- [Visual Studio 的辅助功能 (Windows)](/visualstudio/ide/reference/accessibility-features-of-visual-studio)