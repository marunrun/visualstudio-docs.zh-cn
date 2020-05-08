---
title: 修改对象样式
titleSuffix: Blend for Visual Studio
ms.date: 11/04/2016
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f38bfc7a6899ff1d61b8103204bb58df5c5106a6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "82921123"
---
# <a name="modify-the-style-of-objects-in-blend-for-visual-studio"></a>修改 Blend for Visual Studio 中对象的样式

自定义对象的最简单方法是在“属性”**** 窗格中设置属性。

如果你希望重复使用设置或设置组，请创建可重复使用的资源。 这可以是样式**、模板** 或如自定义颜色一样简单的对象。 还可以使控件基于其状态以不同方式出现。 例如，按钮在用户单击它时变为绿色。

## <a name="brushes-modify-the-appearance-of-an-object"></a>画笔：修改对象的外观

如果要更改对象外观，请向它应用画笔。

### <a name="paint-a-repeating-image-or-pattern-on-an-object"></a>在对象上绘制重复图像或图案

可使用平铺画笔** 在对象上绘制重复图像或图案。

若要创建平铺画笔，请首先创建图像画笔**、图形画笔** 或视觉画笔** 资源。

使用图像创建图像画笔。 下图显示图像画笔、平铺的图像画笔和翻转的图像画笔。

![图像画笔](../designers/media/81f84f56-906d-456b-8288-d77da1e01e31.png) ![平铺图像画笔](../designers/media/d3782ca8-64da-47a4-a095-c6cdd0fa47a2.png) ![翻转图像画笔](../designers/media/38ae3691-f3f1-4a1e-82ca-c7fa164bf56e.png)

使用矢量图形（如路径或形状）创建图形画笔。 下图显示图形画笔、平铺的图形画笔和翻转的图形画笔。

![图形画笔](../designers/media/197666ac-ef57-4c5c-9779-669e991a00a5.png) ![平铺图形画笔](../designers/media/ba09cda3-4cee-40ba-b3d4-edc032158bdc.png) ![翻转图形画笔](../designers/media/15bf6021-620c-4490-9eae-086153d3f14f.png)

通过控件（如按钮）创建视觉画笔。 下图显示视觉画笔和平铺的视觉画笔。

![视觉画笔](../designers/media/fb6c90e0-153c-48fe-b563-e601beac6227.png) ![平铺视觉画笔](../designers/media/e261b99f-7d8f-4d91-bc84-19c7beccc255.png)

## <a name="styles-and-templates-create-a-consistent-look-and-feel-across-controls"></a>样式和模板：跨控件创建一致的外观

可以一次性设计控件的外观和行为，然后将该设计应用于其他控件，以便不必分别进行维护。

是否应使用样式？****：如果只是想设置默认属性（如按钮的颜色），请使用样式**。 即使在应用了样式之后，也可以修改控件。

是否应使用模板？****：如果想要更改控件的结构，请使用模板**。 假设将图形或徽标转换为按钮。 在向控件应用模板之后，无法修改控件。

### <a name="create-a-template-or-style"></a>创建模板或样式

可通过两种方法创建模板。 可以将美工板上的任何对象转换为控件，也可以使模板基于现有控件。

若要将任何对象转换为控件模板，请选择对象，然后在“工具”**** 菜单上，选择“构成控件”****。

如果想要使模板基于现有控件，请选择美工板上的对象。 然后，在美工板顶部，选择痕迹导航按钮，选择“编辑模板”****，然后选择“编辑副本”**** 或“创建空白项”****。

![编辑“模板”菜单](../designers/media/5ebdb33f-aad2-4c10-a328-5e8b04c56a36.png)

若要创建样式，请选择对象，在“对象”**** 菜单上选择“编辑样式”****，然后选择“编辑副本”**** 或“创建空白项”****。

- 选择“编辑副本”**** 可从控件的默认样式或模板开始。

- 选择“创建空白项”**** 可从头开始。

仅当编辑已创建的样式或模板时，"**编辑当前**" 选项才会出现。 对于仍在使用默认系统模板的控件，它不会出现。

在“创建样式资源”**** 对话框中，可以命名样式或模板以便可以在以后使用它，也可以将样式或模板应用于该类型的所有控件。

![“创建样式资源”对话框](../designers/media/4818ee6a-ce60-4b79-91c8-3b1871829eea.png)

> [!NOTE]
> 不能为控件的每种类型都创建样式或模板。 如果控件不支持它们，则痕迹导航按钮不会出现在美工板上方。
> 若要返回到主文档的编辑范围，请单击 "**返回范围" 以** ![将 "](../designers/media/55844eb3-ed98-4f20-aa66-a6f5b23eeb2b.png)作用域返回到" 图标。

### <a name="apply-a-style-or-template-to-a-control"></a>将样式或模板应用于控件

在[对象和时间线](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md#objects-and-timeline-window)窗口中右键单击某个对象，选择“编辑模板”****，然后选择“应用资源”****。

![“应用资源”菜单](../designers/media/dc12debc-7711-47d9-84ce-10322a384397.png)

### <a name="restore-the-default-style-or-template-of-a-control"></a>还原控件的默认样式或模板

选择控件，在 "属性" 窗口中，找到 "**样式**" 或 "**模板**" 属性。 选择“高级选项”，然后在快捷菜单上单击“重置”********。

## <a name="visual-states"></a>可视状态

使用可视状态，可以基于其状态更改控件的外观。 控件可以基于用户交互而具有不同的视觉外观。 例如，可以在用户单击时使按钮变为绿色，也可以运行动画。 可使用过渡缩短或延长可视状态之间的时间。

![鼠标悬停状态](../designers/media/a95c671a-5639-40b9-83db-1e6b214330d5.png)

观看短片：**** ![播放按钮](../designers/media/bldadminconsoleinitialconfigicon.PNG) [管理 WPF 控件的状态](https://www.youtube.com/watch?v=m0PlkF5i6uw)。

## <a name="resources-create-colors-styles-and-templates-and-reuse-them-later"></a>资源：创建颜色、样式和模板，并在以后重复使用它们

可以将项目中的几乎所有对象转换为资源。 资源只是可以在应用程序中的不同位置重复使用的对象。 例如，可以一次性创建一种颜色，使它成为资源，然后在多个对象上使用该颜色。 若要更改所有这些对象的颜色，只需更改该颜色资源。

![将颜色转换为资源按钮](../designers/media/89203705-cf66-46e0-b153-52a23cd744f7.png) ![“创建颜色资源”对话框](../designers/media/6bff8b19-3cd5-41a0-bbf9-ff65532d5aae.png)

## <a name="see-also"></a>另请参阅

- [使用 Blend for Visual Studio 创建 UI](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)
