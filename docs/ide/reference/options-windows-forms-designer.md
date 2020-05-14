---
title: 选项, Windows 窗体设计器, 常规
ms.date: 08/09/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.WindowsFormsDesigner.General
helpviewer_keywords:
- Windows Forms Designer options
- Options dialog box, Windows Forms Designer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 2a72b27dc2277501d0e0957c8b89b551f4d6852d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75568056"
---
# <a name="options-dialog-box-windows-forms-designer"></a>“选项”对话框：Windows Forms Designer — Windows 窗体设计器

使用 Windows 窗体设计器选项页，用户可以在 Visual Studio 中设置 Windows 窗体设计器网格和其他功能的首选项。 可以从“工具”  菜单打开“选项”  对话框。

## <a name="code-generation-settings"></a>代码生成设置

**优化代码生成**\
启用优化代码生成。 一些控件可能与此模式不兼容。 为了使这一更改生效，必须关闭并重新打开 Visual Studio。

## <a name="high-dpi-support"></a>高 DPI 支持

**DPI 缩放通知**\
在 Windows 窗体设计器中显示一条消息，表明可使用 100% 缩放比例来重启 Visual Studio。 有关详细信息，请参阅[禁用 Visual Studio 中的 DPI 感知](/dotnet/framework/winforms/disable-dpi-awareness-visual-studio)。

## <a name="layout-settings"></a>布局设置

**默认网格单元格大小**\
设置设计器上水平网格线和垂直网格线之间的间距（以像素为单位）。 默认大小为 8, 8。 最大大小为 200, 200。

**布局模式**\
指定用于布局的对齐系统。 可以选择 SnapToGrid 或对齐线。

**显示网格**\
指定设计器是否显示大小调整网格。 默认情况下，网格处于打开状态。

**对齐到网格**\
确定设计器是否将对象和控件对齐到网格。 换言之，当启用此功能时，设计器上元素的大小调整和移动都受到 GridSize 增量的限制。 打开 SnapToGrid 可以更容易地精确排列用户界面的各个方面，但无法让用户自由放置控件。 默认情况下，打开 SnapToGrid。

## <a name="object-bound-smart-tag-settings"></a>对象绑定智能标记设置

**自动打开智能标记**\
确定控件和组件是否显示智能标记。 并非所有控件和组件都支持智能标记。

## <a name="refactoring"></a>重构

**启用重命名时重构**\
设置为 `true` 时，从“属性”窗口或“文档大纲”窗口重命名组件时，将执行重命名重构操作。

## <a name="toolbox"></a>工具箱

**自动填充工具箱**\
确定是否使用项目生成的组件和控件自动填充“工具箱”窗口。
