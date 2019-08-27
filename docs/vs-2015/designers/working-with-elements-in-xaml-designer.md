---
title: 在 XAML 设计器中使用元素 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: a29690bf-f212-4ac6-a77a-adc53d14102e
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1ecb5981a8111f3fca013d3b5f115155ac7baf89
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824851"
---
# <a name="working-with-elements-in-xaml-designer"></a>Working with elements in XAML Designer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在 XAML 中、在代码中或使用 XAML 设计器向应用程序中添加元素（控件、布局和形状）。 本主题介绍如何在 Visual Studio 或 Blend for Visual Studio 中使用 XAML 设计器中的元素。  
  
## <a name="adding-an-element-to-a-layout"></a>将元素添加到布局  
 布局是调整元素在 UI 中的大小和位置的过程  。 若要放置可视元素，必须将这些元素置于布局[面板](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.panel.aspx)中。 `Panel` 具有一个子属性，该子属性是 [FrameworkElement](https://msdn.microsoft.com/library/windows/apps/br208706.aspx) 类型的集合。 可使用各种 `Panel` 子元素（如 [Canvas](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.canvas.aspx)[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 和 [Grid](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.grid.aspx)）来充当布局容器以及在页面上放置和排列元素。  
  
 默认情况下，`Grid` 面板用作页面或窗体中的顶级布局容器。 可在顶级页面布局内添加布局面板、控件或其他元素。  
  
#### <a name="to-add-an-element-to-a-layout"></a>若要向布局添加元素，请执行以下操作  
  
- 在 XAML 设计器中，执行以下操作：  
  
  - 双击“工具箱”的某个元素（或选择工具箱中的某个元素，然后按 Enter 键）  。  

  - 将元素从“工具箱”拖到美工板  。  

  - 在“工具箱”中，选择一种绘制工具（例如，[椭圆形](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.shapes.ellipse.aspx)或[矩形](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.shapes.rectangle.aspx)），然后在活动面板上绘制元素  。  
  
## <a name="changing-the-layering-order-of-elements"></a>更改元素的分层顺序  
 当 XAML 设计器中美工板上有两个元素时，一个元素在分层顺序中将显示在另一个元素之前。 文档大纲窗口中的元素列表的底部是最靠前的元素（除了在设置了元素的“ZIndex”属性时）  。 当将元素插入页面、窗体或布局容器时，元素将自动放置在活动容器元素中的其他元素之前。 若要更改元素的顺序，可使用“排序”命令，或将元素拖入文档大纲窗口的对象树中  。  
  
#### <a name="to-change-the-layering-order"></a>若要更改分层顺序，请执行以下操作  
  
- 执行下列操作之一：  
  
  - 在“文档大纲”窗口中，向上或向下拖动元素，以创建所需的分层顺序  。  
  
  - 右键单击文档大纲窗口中或美工板上想要更改其分层顺序的元素，指向“顺序”，然后单击以下选项之一：   
  
    - “置于顶层”：将元素一直移动到顺序的顶层  。  
  
    - “上移一层”，使元素在顺序中上移一层  。  
  
    - “下移一层”，使元素在顺序中下移一层  。  
  
    - “置于底层”：将元素一直移到顺序的底层  。  
  
    更改属性窗口中“布局”部分的“ZIndex”属性   。 对于重叠元素，“ZIndex”属性优先于文档大纲窗口中显示的元素的顺序  。 当元素重叠时，“ZIndex”值较小的元素将显示在前面  。  
  
## <a name="changing-the-alignment-of-an-element"></a>更改元素的对齐方式  
 可以通过使用菜单命令或通过将元素拖到对齐线，对齐美工板中的元素。  
  
 对齐线是一个视觉提示，有助于将某个元素相对于应用中的其他元素进行对齐  。  
  
#### <a name="to-align-two-or-more-elements-by-using-menu-commands"></a>使用菜单命令对齐两个或更多元素  
  
1. 选择要对齐的元素。 可以通过按住 Ctrl 键的同时选择元素选择多个元素。  
  
2. 在属性窗口中“布局”部分的“HorizontalAlignment”下，选择以下属性之一：“左”、“中心”、“右”或“拉伸”       。  
  
3. 在属性窗口中，在“布局”部分的“VerticalAlignment”下，选择以下属性之一：“顶部”、“中心”、“底部”或“拉伸”     ,   。  
  
#### <a name="to-align-two-or-more-elements-by-using-snaplines"></a>使用对齐线对齐两个或更多元素  
  
- 在 XAML 设计器中，在含有至少两个元素的布局中，拖动其中一个元素或调整其大小，以使其边缘与另一个元素对齐。  
  
     当边缘对齐时，将显示“对齐边界”以指示对齐方式  。 对齐边界显示为红色虚线。 仅当启用了“对齐线对齐”  时，才会显示对齐边界。 有关显示对齐边界的美工板图示，请参阅[使用 XAML 设计器创建 UI](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)。  
  
## <a name="changing-the-an-elements-margins"></a>更改元素的边距  
 XAML 设计器中的边距决定了美工板上元素周围的空白区域的大小。 例如，边距指定元素外边缘与包含该元素的 `Grid` 面板的边界之间空白区域的大。 边距还指定 `StackPanel` 中包含的元素之间空白区域的大小。  
  
#### <a name="to-change-an-elements-margins-in-the-properties-window"></a>在“属性”窗口中更改元素边距的步骤  
  
1. 选择要更改边距的元素。  
  
2. 在属性窗口中的“布局”下，更改任何“边距”属性（“顶部”、“左”、“右”或“底部”）的值（以像素为单位或与设备无关的单位，大约 1/96 英寸）       。  
  
#### <a name="to-change-an-elements-margins-in-the-artboard"></a>若要更改美工板中元素的边距，请执行以下操作  
  
- 若要更改元素相对于其布局容器的边距，请在元素处于选中状态且位于布局容器内时，单击美工板中元素周围出现的“边距装饰器”  。 有关显示边距装饰器的图示，请参阅[使用 XAML 设计器创建 UI](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)。  
  
     如果边距装饰器以垂直或水平方向打开，则未设置相应的边距。 如果边距装饰器关闭，则已设置相应的边距。  
  
     当打开边距装饰器而未设置相反边距时，请根据美工板中的元素的位置，将相反边距设置为正确的值。 对于相反的边距（如“左侧”和“右侧”边距），将始终至少设置一个属性   。  
  
    > [!IMPORTANT]
    > 置于某些布局容器内的元素（如 <xref:Windows.UI.Xaml.Controls.Canvas>）没有边距装饰器。 置于 <xref:Windows.UI.Xaml.Controls.StackPanel> 内的元素对于左边距和右边距或上边距和下边距有边距装饰器，具体取决于 `StackPanel` 的方向。  
  
## <a name="grouping-and-ungrouping-elements"></a>对元素进行分组和取消分组  
 对 XAML 设计器中的两个或更多元素进行分组可创建一个新的布局容器，然后将这些元素置于该容器内。 通过将两个或更多元素一起置于一个布局容器中，可轻松地选择、移动和转换该组，如同该组中的所有元素是一个元素。 对于识别以某种方式相互关联的元素（如组成导航元素的按钮），分组也很有用。 对元素进行取消分组时，只需删除包含这些元素的布局容器即可。  
  
#### <a name="to-group-elements-into-a-new-layout-container"></a>若要将元素组成新的布局容器，请执行以下操作  
  
1. 选择要分组的元素。 （若有选择多个元素，请按下并按住 Ctrl 键并同时单击这些元素。）  
  
2. 右键单击选定的元素，指向“分组”，然后单击想要在其中放置该组的布局容器的类型  。  
  
    > [!TIP]
    > 如果选择 <xref:Windows.UI.Xaml.Controls.Viewbox><xref:Windows.UI.Xaml.Controls.Border>, 或 <xref:Windows.UI.Xaml.Controls.ScrollViewer> 来分组元素，则元素将被放置于 <xref:Windows.UI.Xaml.Controls.Viewbox>、<xref:Windows.UI.Xaml.Controls.Border> 或 <xref:Windows.UI.Xaml.Controls.ScrollViewer> 内的一个新 <xref:Windows.UI.Xaml.Controls.Grid> 面板中。 如果在其中某个布局容器中对元素进行取消分组，则仅删除 <xref:Windows.UI.Xaml.Controls.Viewbox>、<xref:Windows.UI.Xaml.Controls.Border> 或 <xref:Windows.UI.Xaml.Controls.ScrollViewer>，而保留 <xref:Windows.UI.Xaml.Controls.Grid> 面板。 若要删除 `Grid` 面板，请再次对这些元素进行取消分组。  
  
#### <a name="to-ungroup-elements-and-delete-the-layout"></a>若要对元素进行取消分组并删除布局，请执行以下操作  
  
- 右键单击想要取消分组的组并单击“取消分组”  。  
  
  还可以通过右键单击文档大纲窗口中选定的项，然后单击“分组”或“取消分组”，以对元素进行分组或取消分组   。  
  
## <a name="resetting-the-element-layout"></a>重置元素布局  
 可以通过使用“布局重置”命令还原某个元素特定布局属性的默认值。 通过使用此命令可重置元素的边距、对齐方式、宽度、高度和大小，个别重置或同时全部重置均可。  
  
#### <a name="to-reset-the-element-layout"></a>若要重置元素布局，请执行以下操作  
  
- 在文档大纲窗口或美工板中，右键单击该元素，选择“布局”、“重置”、PropertyName，其中 PropertyName 是想要重置的属性（或者选择“布局”、“全部重置”，重置该元素的所有布局属性）       。  
  
## <a name="see-also"></a>另请参阅  
 [使用 XAML 设计器创建 UI](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
