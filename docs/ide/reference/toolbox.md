---
title: 工具箱窗口
ms.date: 06/01/2020
ms.topic: reference
f1_keywords:
- vs.toolbox.general
- vs.toolbox
helpviewer_keywords:
- Toolbox [Visual Studio]
- custom controls [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9807762a4573cdbc68a4af26bf9d73b46827c7af
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285320"
---
# <a name="toolbox"></a>工具箱

“工具箱”窗口显示可以添加到 Visual Studio 项目的控件。 若要打开“工具箱”，请在菜单栏中依次选择“视图” > “工具箱”，或按 Ctrl+Alt+X。

![“工具箱”窗口](media/vs-2019/toolbox.png "“工具箱”窗口的屏幕截图")

还可以将不同的控件拖到和放置到你使用的设计器的图面上，然后调整控件的大小并将它们定位。

“工具箱”与设计器视图一起显示，如 XAML 文件或 Windows 窗体应用项目的设计器视图。 “工具箱”仅显示可在当前设计器中使用的控件。 若要进一步筛选所显示的项，可以搜索“工具箱”。

> [!NOTE]
> 对于一些项目类型，“工具箱”可能不会显示任何项。

项目定目标到的 .NET 版本也会影响工具箱中显示的控件集。 如有必要，可从项目的属性页更改目标框架版本。 在“解决方案资源管理器”中选择项目节点，再在菜单栏上依次选择“项目” > “项目名属性”  。 在“应用程序”选项卡上，使用“目标框架”下拉列表。

::: moniker range="vs-2019"

![“工具箱”窗口](media/vs-2019/toolbox-change-dotnet-version.png "可以在其中更改 .NET 版本的对话框的屏幕截图")

::: moniker-end

## <a name="manage-the-toolbox-window-and-its-controls"></a>管理“工具箱”窗口及其控件

默认情况下，“工具箱”在 Visual Studio IDE 左侧折叠，并在光标移到它上面时显示。 可固定“工具箱”（通过单击工具栏上的“固定” 图标），这样它就可以在光标移动时仍一直处于打开状态。 也可以取消停靠“工具箱”窗口，并将它拖到屏幕上的任何位置。 若要停靠、取消停靠和隐藏“工具箱”，可以右键单击它的工具栏，并选择其中一个选项。

> [!TIP]
> 如果“工具箱”不再在 Visual Studio IDE 左侧折叠，可以通过在菜单栏中依次选择“窗口” > “重置窗口布局”来重新添加它。

若要重新排列“工具箱”选项卡中的项，或添加自定义选项卡和项，可以使用右键单击关联菜单中的下列命令：

- 重命名项 - 重命名所选的项。

- 列表视图 - 显示垂直列表中的控件。 如果未选中，则这些控件水平显示。

- 显示所有 - 显示所有可能的控件（不只是适用于当前设计器的控件）。

- 选择项 - 打开“选择工具箱项”对话框即可指定“工具箱”中显示的项 。 可以通过选中或清除复选框显示或隐藏项。

- 按字母顺序对项排序 - 按名称对项排序。

- 重置工具栏 - 还原默认“工具箱”设置和项。

- 添加选项卡 - 添加新的“工具箱”选项卡。

- 上移 - 将所选项上移。

- 下移 - 将所选项下移。

## <a name="create-and-distribute-custom-toolbox-controls"></a>创建和分发自定义“工具箱”控件

可以从基于 [Windows Presentation Foundation](../../extensibility/creating-a-wpf-toolbox-control.md) 或 [Windows 窗体](../../extensibility/creating-a-windows-forms-toolbox-control.md)的项目模板入手，创建自定义“工具箱”控件。 然后，可以使用[“工具箱”控件安装程序](https://download.microsoft.com/download/8/3/6/836657BD-9CCB-4ED4-B9D2-FB769473B284/TCI_whitepaper.docx)，将自定义控件分发给团队成员或发布到网上。

## <a name="next-steps"></a>后续步骤

若要详细了解一些可用的“工具箱”选项卡，请单击以下链接：

- [“工具箱”->“数据”选项卡](../../ide/reference/toolbox-data-tab.md)
- [“工具箱”->“组件”选项卡](../../ide/reference/toolbox-components-tab.md)
- [“工具箱”->“HTML”选项卡](../../ide/reference/toolbox-html-tab.md)

## <a name="see-also"></a>请参阅

- [“选择工具箱项”、“WPF 组件”](choose-toolbox-items-wpf-components.md)
