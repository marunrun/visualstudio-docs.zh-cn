---
title: 在 XAML 设计器中将对象组织到布局容器中
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 29c80c38-0fa3-48d6-b3a8-3b864f482e44
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 3f05874459553b0b83c5e43f326a5deb6b0d4798
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "82921105"
---
# <a name="organize-objects-into-layout-containers-in-xaml-designer"></a>在 XAML 设计器中将对象组织到布局容器中

本文介绍用于 XAML 设计器的版式面板和控件。

想象你希望对象出现在页面上的哪个位置&mdash;诸如图像、按钮和视频等对象。 也许你希望它们出现在行和列中、在单个行中（垂直或水平）或在固定位置中。

在考虑好页面的显示情况后，请选择布局面板。 所有页面都从一个布局面板开始，因为你需要某个容器来向其中添加对象。 默认情况下，它是一个**网格**，但你可以更改它。

布局面板可帮助你在页面上排列对象，但是它们的作用不仅于此。 它们可以帮助你针对不同屏幕大小和分辨率进行设计。 当用户运行你的应用时，布局面板中的所有对象都会调整大小以匹配用户设备的屏幕空间。 当然，如果你不希望布局这样做，则可以为布局的一部分或整个布局重写该行为。 可以使用高度和宽度属性对此进行控制。

## <a name="layout-panels"></a>布局面板

通过选择这些布局面板之一来开始设计你的页面。 页面可以具有多个布局面板。 例如，可从 Grid**** 布局面板开始，然后将一个 StackPanel**** 添加到 Grid**** 中的某个区域，即可在该元素中垂直排列控件。

以下布局面板是最常用的，不过还有一些其他布局面板。 在 Visual Studio 的“工具箱”中或 Blend for Visual Studio 的“资产”面板中可以找到它们********。

### <a name="grid"></a>Grid

在行和列中排列对象。

![Grid 版式面板](../designers/media/98b234b2-ac3b-441f-9136-98375fee87b7.png)

### <a name="uniformgrid"></a>UniformGrid

将对象排列到相等或统一的网格区域中。 此面板非常适用于排列图像的列表。

（仅适用于 WPF 项目。）

![UniformGrid 版式面板](../designers/media/928b9284-a7e8-4678-875a-656b80b78076.png)

### <a name="canvas"></a>Canvas

按任何所需方式排列对象。 当用户运行你的应用时，这些元素将在屏幕上具有固定位置。

![Canvas 版式面板](../designers/media/e1ae27f0-3a57-454e-b580-877dcea8836d.png)

### <a name="stackpanel"></a>StackPanel

在单个行中水平或垂直排列对象。

![StackPanel 版式面板](../designers/media/a85a7b57-b0a8-495e-b985-f0291e41d093.png)

### <a name="wrappanel"></a>WrapPanel

按顺序从左到右排列对象。 面板最右边空间不足时，它会将内容换行** 到下一行，并采用从左到右、从上到下的换行顺序。 还可以使自动换行面板的方向垂直，以便对象从上到下、从左到右排列。

（仅适用于 WPF 项目。）

![WrapPanel 版式面板](../designers/media/b1c415fb-9a32-4a18-aa0b-308fca994ac9.png)

### <a name="dockpanel"></a>DockPanel

排列对象，使它们停留或停靠在面板的一个边缘**。

（仅适用于 WPF 项目。）

![DockPanel 版式面板](../designers/media/72d46b58-9a49-4dd5-8af7-6843c0440226.png)

**观看简短视频：** !["播放"](../designers/media/bldadminconsoleinitialconfigicon.PNG)按钮[WPF-system.windows.controls.dockpanel>](https://www.youtube.com/watch?v=EBH_OIM-zPo)

## <a name="layout-controls"></a>布局控件

也可以向布局控件添加对象。 布局控件功能不如布局面板那么丰富，在某些情况中这些控件可能很有用。

以下布局控件是最常用的，不过还有一些其他布局控件。 在 Visual Studio 的“工具箱”中或 Blend for Visual Studio 的“资产”面板中可以找到它们********。

### <a name="border"></a>Border

围绕创建边框、背景或两者。 只能将一个对象添加到边框****。 如果要将边框或背景应用于多个对象，请将布局面板添加到边框****。 然后，将对象添加到该面板或控件。

![边框布局控件](../designers/media/e761238b-99fd-43c5-bbc4-57538b8289ff.png)

### <a name="popup"></a>弹出项

在窗口中向用户显示信息或选项。 只能将一个对象添加到弹出项****。 默认情况下，弹出项**** 包含一个 Grid****，但是可以更改。

### <a name="scrollviewer"></a>ScrollViewer

使用户可以向下滚动页面或页面区域。 只能将一个对象添加到 ScrollViewer****，因此添加 Grid**** 或 StackPanel**** 等布局面板很有必要。

![ScrollViewer 布局控件](../designers/media/06b326d4-f23d-41a6-b26b-e1aff37572a7.png)

### <a name="viewbox"></a>Viewbox

采用与缩放控件十分类似的方式扩展对象。 只能将一个对象添加到 Viewbox****。 如果要将该效果应用于多个对象，请将布局面板添加到 ViewBox****，然后将控件添加到该布局面板。

（仅适用于 WPF 项目。）

![ViewBox 布局控件](../designers/media/f5b13c66-d918-4141-8a16-bd8f8628687a.png)

## <a name="see-also"></a>另请参阅

- [在 XAML 设计器中使用元素](../xaml-tools/working-with-elements-in-xaml-designer.md)
- [使用 XAML 设计器创建 UI](../xaml-tools/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
