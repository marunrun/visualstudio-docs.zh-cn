---
title: 选择工具箱项，WPF 组件
ms.date: 06/21/2017
ms.topic: reference
f1_keywords:
- vs.chooseitems.wpfcomponents
helpviewer_keywords:
- WPF Components tab, Choose Toolbox Items dialog box
- Choose Toolbox Items dialog box, WPF Components tab
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c3de8e1d83a5d74f518eda2d5ab59bd9845b45a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72630868"
---
# <a name="choose-toolbox-items-wpf-components"></a>“选择工具箱项”->“WPF 组件”

“选择工具箱项”  对话框中的此选项卡显示了在本地计算机上可用的 Windows Presentation Foundation (WPF) 控件列表。 若要显示此列表，请从“工具”  菜单中选择“选择工具箱项”  ，从而显示“选择工具箱项”  对话框，然后选择其中的“WPF 组件”  选项卡。若要对所列组件排序，请选择任意列标题。

- 选中组件旁边的复选框后，该组件的图标将显示在“工具箱”  中。

    > [!TIP]
    > 若要将 WPF 控件添加到打开以供编辑的项目文档，请将它的“工具箱”  图标拖到“设计”视图图面。 组件的默认标记和代码将插入到项目中，以便进行修改。 有关详细信息，请参阅[工具箱](../../ide/reference/toolbox.md)。

- 清除组件旁边的复选框后，将从“工具箱”  中删除相应的图标。

    > [!NOTE]
    > 计算机上安装的 .NET 组件仍然可用，无论其图标是否显示在“工具箱”中  。

“WPF 组件”  选项卡上的列包含下列信息：

**Name**

列出计算机注册表中条目的 WPF 控件的名称。

**命名空间**

显示定义组件结构的 [.NET API](/dotnet/api/?view=netframework-4.7) 命名空间的层次结构。 对此列排序可列出计算机上安装的每个 .NET 命名空间中的可用组件。

**程序集名称**

显示包含每个组件的命名空间的 .NET 程序集的名称。 对此列排序可列出计算机上安装的每个 .NET 程序集中包含的命名空间。

**目录**

显示 .NET 程序集的位置。 所有程序集的默认位置是全局程序集缓存。 有关全局程序集缓存的详细信息，请参阅[使用程序集和全局程序集缓存](/dotnet/framework/app-domains/working-with-assemblies-and-the-gac)。

## <a name="uielement-list"></a>UIElement 列表

### <a name="filter"></a>筛选器

基于文本框中提供的字符串筛选 WPF 控件列表。 将显示四列中的所有匹配项。

**清除**

清除筛选字符串。

**浏览**

开启“打开”  对话框，这可导航到包含 WPF 控件的程序集。 将其用于加载不在全局程序集缓存中的程序集。

**语言**

显示包含所选 WPF 控件的程序集的本地化语言。

## <a name="limitations"></a>限制

向工具箱添加自定义控件或 <xref:System.Windows.Controls.UserControl> 具有以下限制：

- 仅适用于在当前项目外部定义的自定义控件。

- 如果将解决方案配置从“调试”更改为“发布”，或从“发布”更改为“调试”，则不能正确更新。 这是因为该引用不是项目引用，而是磁盘上的程序集引用。 如果控件属于当前解决方案，从“调试”更改为“发布”时，项目将继续引用该控件的调试版本。

此外，如果将设计时元数据应用到自定义控件，而且此元数据指定将 [Microsoft.Windows.Design.ToolboxBrowsableAttribute](/previous-versions/visualstudio/visual-studio-2010/bb547991(v=vs.100)) 设置为 `false`，则该控件不会出现在“工具箱”中。

可以通过映射控件的命名空间和程序集，直接在 XAML 视图中引用控件。

## <a name="see-also"></a>请参阅

- [工具箱](../../ide/reference/toolbox.md)
- [WPF 入门](../../designers/getting-started-with-wpf.md)
