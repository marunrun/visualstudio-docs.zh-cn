---
title: 可访问性
description: 本文介绍 Visual Studio for Mac 中的辅助功能及其启用方法。
author: conceptdev
ms.author: crdun
ms.date: 04/17/2019
ms.assetid: 2C4AAC2E-3B4A-4496-8BE0-1F5A7F81D1CA
ms.openlocfilehash: 13b8d40a6ab31d7178e95a3896afa1c85c804f6c
ms.sourcegitcommit: a124076dfd6b4e5aecda4d01984fee7b0c034745
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68787643"
---
# <a name="accessibility"></a>可访问性

Visual Studio for Mac 提供下列辅助功能，旨在更方便残障人士使用：

- Solution Pad 和 Editor Pad 中的文本放大选项
- 编辑器中的文本大小选项
- 编辑器中的颜色自定义
- 键盘导航
- 快捷方式自定义
- 支持对方法和参数使用代码完成功能

除了这些功能，Apple 还提供多种工具来满足用户的特殊需求，如 VoiceOver 和语音听写。

若要详细了解 macOS 中的辅助功能，请访问 [Apple 网站](https://www.apple.com/accessibility/mac/)。

## <a name="enabling-macos-assistive-technologies-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中启用 macOS 辅助技术

默认情况下，Visual Studio for Mac 对 macOS 辅助技术的支持处于禁用状态。 若要启用该支持，请执行以下步骤：

1. 依次转到“Visual Studio(菜单)”>“首选项”>“其他”>“辅助功能” 

2. 选中“启用辅助功能”  复选框：

   ![“辅助功能首选项”复选框](media/accessibility-preferences.png)

3. 选择“重新启动 Visual Studio”  按钮以重新启动 Visual Studio 并启用对 Apple 辅助技术的支持。

## <a name="how-to-use-keyboard-navigation"></a>如何：使用键盘导航

键盘导航支持直接内置于 macOS 中，但为了获得最全面的体验，应将 macOS 设置为浏览所有控件  ：

![系统首选项 - 键盘 - 所有控件](media/accessibility-preferences-keyboard.png)

通过将“键盘完全访问”  设置为“所有控件”  ，可以在窗口或对话框中浏览所有控件。 然后，可以使用下列方法之一选择控件：

- 按 Tab 前移切换控件
- 按 Shift-Tab 后移切换控件
- 按箭头键沿箭头方向切换控件
- 按 Control-Tab 移出文本区域框
- 按空格键激活当前焦点所在的控件。

## <a name="how-to-enable-and-use-voiceover"></a>如何：启用和使用 VoiceOver

若要启用或禁用 VoiceOver，请按“&#8984; + F5” 

VoiceOver 命令在本指南中显示为“VO+_key_”，其中 VO 指的是“VoiceOver 实用工具”应用程序中设置的修饰符    。 默认修饰符为“Ctrl + Alt”  。例如，根据 VoiceOver 修饰符，“VO + M”  表示“Ctrl + Alt + M”  。为简洁起见，光标键将称为“左”、“右”   等。

若要浏览 Visual Studio for Mac 用户界面，请使用以下组合键：

- **VO + 右/左**：在用户界面元素之间导航
  - VoiceOver 将发布控件的标签和类型，并说明如何与之交互。
- **VO + Shift + 上/下**：单步执行/跳出元素
  - 处于元素中后，就可以使用“VO + 左/由”  浏览其中的元素。
- **VO + 空格键**：选择控件/与控件交互
- **VO + M**：与 Visual Studio for Mac 菜单栏交互

有关使用 VoiceOver 和命令的完整列表的详细信息，请参阅以下指南：

- [Apple VoiceOver 入门指南](https://support.apple.com/en-us/guide/voiceover-guide/welcome/web)
- [macOS 中的 VoiceOver 命令](http://lab.dotjay.com/notes/voiceover-commands/)

## <a name="see-also"></a>请参阅

- [Visual Studio 的辅助功能 (Windows)](/visualstudio/ide/reference/accessibility-features-of-visual-studio)
