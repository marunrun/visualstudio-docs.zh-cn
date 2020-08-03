---
title: XAML 设计器概述
ms.date: 03/03/2020
ms.topic: conceptual
f1_keywords:
- VS.XamlDesigner
- VS.DevicePanel
- VS.XamlEditor
- VS.DocumentOutline
- Blend.Start.Dev12
ms.devlang: CSharp
ms.assetid: c54969a7-d75a-4a35-9b37-af7a596a7c24
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: f8579a4e8088dc0fc6e7403da7f0371e46f2c928
ms.sourcegitcommit: e359b93c93c6ca316c0d8b86c2b6e566171fd1ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2020
ms.locfileid: "87507958"
---
# <a name="create-a-ui-by-using-xaml-designer"></a>使用 XAML 设计器创建 UI

Visual Studio 和 Blend for Visual Studio 中的 XAML 设计器提供了一个可视化界面，可帮助您设计基于 XAML 的应用程序，如 WPF 和 UWP。 可以通过拖动“工具箱”窗口（Blend for Visual Studio 中的“资产”窗口）中的控件，并在“属性”窗口中设置属性，为应用创建用户界面。 还可以直接在 XAML 视图中编辑 XAML。

对于高级用户，甚至可以[自定义 XAML 设计器](https://github.com/microsoft/xaml-designer-extensibility/blob/master/documents/xaml-designer-extensibility-migration.md)。

> [!NOTE]
> Xamarin。窗体不支持 XAML 设计器。 若要查看 Xamarin. Forms XAML Ui 并在应用程序运行时对其进行编辑，请使用适用于 Xamarin 的 XAML 热重载。 有关详细信息，请参阅[适用于 Xamarin 的 XAML 热重载（预览）](/xamarin/xamarin-forms/xaml/hot-reload/)页。

## <a name="xaml-designer-workspace"></a>XML 设计器工作区

XAML 设计器中的工作区由若干可视界面元素组成。 其中包括美工板**（属于可视化设计图面）、XAML 编辑器、“文档大纲”窗口（Blend for Visual Studio 中的“对象和时间线”窗口）和“属性”窗口。 若要打开 XAML 设计器，请右键单击“解决方案资源管理器” **** 中的 XAML 文件，然后选择“视图设计器” ****。

XAML 设计器提供 XAML 视图和应用程序呈现的 XAML 标记的同步设计视图。 打开 Visual Studio 或 Blend for Visual Studio 中的某个 XAML 文件后，可以通过使用“设计”**** 和“XAML”**** 选项卡，在“设计”视图和“XAML”视图之间进行切换。 可以使用“交换窗格” **** 按钮 ![XAML 设计器中的“交换窗格”按钮](media/swap-panes.PNG)，切换显示于顶部的窗口：美工板或 XAML 编辑器。

### <a name="design-view"></a>设计视图

在“设计”视图，包括美工板的窗口是活动窗口，并且可以将其用作主要工作台面。 可通过添加、绘制或修改元素，在应用中用于直观地设计页面。 有关详细信息，请参阅[使用 XAML 设计器中的元素](../xaml-tools/working-with-elements-in-xaml-designer.md)。 此图显示了“设计”视图中的美工板。

![XAML 设计器的设计视图](media/xaml-artboard.png)

这些功能在美工板中可用：

**对齐线**

对齐线是显示为红色虚线的对齐边界，在控件的边缘对齐时或文本基线对齐时进行显示。** 仅当启用了“对齐线对齐” **** 时，才会显示对齐边界。

**网格轨道**

使用网格轨道可以管理[网格](xref:Windows.UI.Xaml.Controls.Grid)面板中的行和列。 可以创建和删除行和列，并可以调整其相对宽度和高度。 显示在美工板左侧的垂直网格轨道用于行，而显示在顶部的水平线则用于列。

**网格装饰器**

网格装饰器显示为三角形，在网格轨道上它附加有垂直线或水平线。 拖动网格装饰器时，相邻的列或行的宽度或高度随鼠标的移动而改变。

网格装饰器用于控制网格的行和列的宽度和高度。 可以通过单击网格轨道，添加新列或行。 当为具有两个或多个列或行的网格面板添加新行或列时，轨道外将显示一个小型工具栏，可显式设置宽度和高度。 小型工具栏使你能够为网格行和列设置调整大小选项。

![XAML 设计器中的网格装饰器](media/grid-adorner.png)

**重设句柄大小**

重设句柄大小显示在所选控件上，使你能够调整控件的大小。 当调整控件大小时，通常会出现宽度和高度值，帮助设置控件的大小。 有关在“设计”视图中操作控件的详细信息，请参阅[使用 XAML 设计器中的元素](../xaml-tools/working-with-elements-in-xaml-designer.md)****。

**边距**

边距表示控件边缘与其容器边缘之间的固定空间量。 可使用“属性”窗口中“布局”下的 [Margin](xref:Windows.UI.Xaml.FrameworkElement.Margin) 属性来设置控件的边距********。

**边距装饰器**

使用边距装饰器更改元素相对于其布局容器的边距。 打开边距装饰器，未设置边距时，边距装饰器将显示断开的锁链。 未设置边距时，元素在运行时调整布局容器的大小时保留在原处。 边距装饰器关闭时，边距装饰器将显示完好的锁链，且在运行时调整布局容器的大小时，元素随边距一起移动（边距保持固定）。

**元素句柄**

当将指针移动到环绕某元素的蓝色方框的角落时，可以通过使用显示于美工板上的元素句柄修改元素。 利用这些句柄可以旋转、调整大小、翻转、移动或向元素添加圆角半径。 元素句柄的符号因函数而异，且根据指针的确切位置进行更改。 如果看不到元素句柄，请确保已选定该元素。

在“设计”视图中，其他美工板命令在窗口的左下角区域可用，如下所示****：

![设计视图命令](media/xaml-design-view-controls.png)

此工具栏上的这些命令可用：

**缩放**

缩放能够确定设计图面的大小。 可以从 12.5% 缩放到 800%，或选择如“适应所选内容”**** 和“适合全部”**** 之类的选项。

**显示/隐藏对齐网格**

显示或隐藏显示网格线的对齐网格。 当启用“网格线对齐”或“对齐线对齐”时，将使用网格线********。

**开启/关闭网格线对齐**

如果已启用 "**网格线对齐**"，则当您将元素拖到美工板上时，它会与最近的水平和垂直网格线对齐。

**切换美工板背景**

在浅色和深色背景之间切换。

**开启/关闭对齐线对齐**

对齐线有助于控件彼此对齐。 如果已启用了“对齐线对齐” **** ，则当相对于其他控件拖动某个控件时，在某些控件的边缘和文本水平或垂直对齐时，将显示对齐边界。 对齐边界显示为红色虚线。

**禁用项目代码**

禁用[项目代码](debugging-or-disabling-project-code-in-xaml-designer.md)（例如，自定义控件和值转换器），并重新加载设计器。

### <a name="xaml-view"></a>XAML 视图

在**xaml**视图中，包含 xaml 编辑器的窗口是活动窗口，而 xaml 编辑器是主要创作工具。 可扩展应用程序标记语言 (XAML) 提供基于 XML 的声明性词汇，用于指定应用程序的用户界面。 XAML 视图包括 IntelliSense、自动格式设置、语法突出显示和标记导航。 下图显示打开了 IntelliSense 菜单的 XAML 视图：

![XAML 视图](media/xaml-editor.png)

## <a name="document-outline-window"></a>“文档大纲”窗口

Visual Studio 中的“文档大纲”窗口类似于 Blend for Visual Studio 中的[对象和时间线](creating-a-ui-by-using-blend-for-visual-studio.md#objects-and-timeline-window)窗口。 “文档大纲”有助于执行以下任务：

- 查看美工板上所有元素的层次结构。

- 选择元素，以便可以修改它们。 例如，你可以在层次结构中移动它们或在属性窗口中设置其属性。 有关详细信息，请参阅[使用 XAML 设计器中的元素](../xaml-tools/working-with-elements-in-xaml-designer.md)。

- 创建和修改控件元素的模板。

- [创建动画](animate-objects-in-xaml-designer.md)（仅 Blend for Visual Studio）。

若要在 Visual Studio 中查看 "文档大纲" 窗口，请在菜单栏上选择 "**查看**  >  **其他窗口**  >  **文档大纲**"。
若要查看 Blend for Visual Studio 中的 "对象和时间线" 窗口，请在菜单栏上选择 "**查看**  >  **文档大纲**"。

![Visual Studio 中的“文档大纲”窗口](media/document-outline-window.png)

“文档大纲/对象和时间线”窗口中的主视图采用树结构显示文档的层次结构。 可以使用文档大纲的层次结构性质检查不同级别的文档的详细信息，单个或成组地锁定和隐藏元素。 "文档大纲/对象和时间线" 窗口中提供了以下选项：

**显示/隐藏**

显示或隐藏美工板元素。 显示时显示为眼睛符号。 还可以按**ctrl** + **h**隐藏元素，按**Shift** + **ctrl** + **h**显示元素。

**锁定/解锁**

锁定或解锁美工板元素。 不能修改已锁定的元素。 锁定时显示为挂锁符号。 还可以按**ctrl** + **+** 来锁定某个元素，按住**Shift**并 + **Ctrl** + **L**将其解锁。

**返回到 pageRoot 范围**

“文档大纲/对象和时间线”窗口顶部的选项显示向上箭头符号，可移到之前的范围。 仅当在样式或模板的范围中时，范围向上可用。

## <a name="properties-window"></a>“属性”窗口

"**属性**" 窗口可用于设置控件的属性值。 它的外观如下所示：

![“属性”窗口](media/xaml-designer-properties-window.png)

"**属性**" 窗口顶部有多种选项：

- 在“名称”框中更改当前所选元素的名称****。
- 在左上角，有一个表示当前所选元素的图标。
- 若要按类别或按字母顺序排列属性，请单击“类别” ****、“名称” **** 或“排列方式” **** 列表中的“源” **** 。
- 若要查看控件的事件列表，请单击“事件”**** 按钮，该按钮显示为一个闪电形符号。
- 若要搜索某个属性，请在搜索框中键入该属性的名称。 在键入时，"**属性**" 窗口将显示与您的搜索匹配的属性。

某些属性允许通过选择向下箭头按钮设置高级属性。

每个属性值的右侧是一个“属性标记” ** ，显示为一个方框符号。 属性标记的外观指示是否有数据绑定到或有资源应用于该属性。 例如，白色方框符号指示默认值，黑色方框符号通常指示已应用某个本地资源，而橙色方框通常指示已应用某个数据绑定。 单击属性标记时，可以导航到一种样式的定义、打开数据绑定生成器或打开资源选取器。

有关使用属性和处理事件的详细信息，请参阅[控件和模式简介](/windows/uwp/design/controls-and-patterns/controls-and-events-intro)。

## <a name="see-also"></a>另请参阅

- [在 XAML 设计器中使用元素](../xaml-tools/working-with-elements-in-xaml-designer.md)
- [如何创建和应用资源](../xaml-tools/how-to-create-and-apply-a-resource.md)
- [演练：在 XAML 设计器中绑定数据](../xaml-tools/walkthrough-binding-to-data-in-xaml-designer.md)
