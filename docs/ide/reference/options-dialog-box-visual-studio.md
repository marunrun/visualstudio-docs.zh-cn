---
title: “选项”对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.toolsoptionspages
helpviewer_keywords:
- Tools Options settings
- Options dialog box
- Options dialog box, development environment
- tools [Visual Studio], customizing
ms.assetid: 02b09877-1df1-4531-a0d1-a4ca17c7f857
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 068c80221a572747ab99e41e78945fe55c57c451
ms.sourcegitcommit: da7f093db52df5dcd67e0a030e616b307f0dc2a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91211256"
---
# <a name="options-dialog-box-visual-studio"></a>“选项”对话框 (Visual Studio)

使用“选项”  对话框，可根据需要配置集成开发环境 (IDE)。 例如，可以为项目建立默认保存位置、更改 Windows 的默认外观和行为以及为常用命令创建快捷方式。 还有特定于开发语言和平台的选项。 可从“工具”菜单中访问“选项”。

## <a name="layout-of-the-options-dialog-box"></a>“选项”对话框的布局

“选项”  对话框分为两部分：左侧的导航窗格和右侧的显示区域。 导航窗格中的树控件包括文件夹节点，例如环境、文本编辑器、项目和解决方案以及源控件。 展开任意文件夹节点以列出其包含的选项页面。 为特定页面选择节点时，其选项将显示在显示区域中。

在一个 IDE 功能加载到内存之前，该功能的选项不会显示在导航窗格中。 因此，如果在结束一个会话的同时开始一个新的会话，可能不会显示之前的选项。 创建项目或运行使用特定应用程序的命令时，相关选项的节点将添加到“选项”对话框中。 只要 IDE 功能保留在内存中，这些添加的选项将保持可用。

> [!NOTE]
> 某些设置集合会限定显示在“选项”对话框的导航窗格中的页面数。

## <a name="how-options-are-applied"></a>如何应用选项

在“选项”**** 对话框中单击“确定”将保存所有页面上的所有设置。 单击任意页面上的“取消”将取消所有更改请求，包括刚刚在其他“选项”**** 页面上所做的更改。 对选项设置（例如[“字体和颜色”、“环境”、“选项”对话框](../../ide/reference/fonts-and-colors-environment-options-dialog-box.md)）所做的某些更改只有在关闭并重新打开 Visual Studio 后才会生效。

## <a name="see-also"></a>请参阅

- [自定义编辑器](../how-to-change-text-case-in-the-editor.md)
