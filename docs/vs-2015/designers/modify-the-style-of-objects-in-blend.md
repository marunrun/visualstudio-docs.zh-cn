---
title: 修改 Blend 中对象的样式 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 31192d2c-5b84-41bc-94c0-898638c170bd
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a5ca94c88a1f131065b7d5de57e9cdc200696d58
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681441"
---
# <a name="modify-the-style-of-objects-in-blend"></a>修改 Blend 中对象的样式
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

自定义对象的最简单方法是在“属性”窗格中设置属性。  
  
 如果你希望重复使用设置或设置组，请创建可重复使用的资源。 这可以是样式、模板或如自定义颜色一样简单的对象。 还可以使控件基于其状态以不同方式出现。 例如，按钮在用户单击它时变为绿色。  
  
 **主题内容**：  
  
- [画笔：修改对象的外观](#Brushes)  
  
- [样式和模板：在控件之间创建一致的外观](#Styles)  
  
- [可视状态：更改基于其状态的控件的外观](#Visual)  
  
- [资源：创建颜色、 样式和模板并重复使用它们更高版本](#Resources)  
  
## <a name="Brushes"></a> 画笔：修改对象的外观  
 如果要更改对象外观，请向它应用画笔。  
  
 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [画笔编辑器](http://www.popscreen.com/v/6A4mO/Microsoft-Expression-Blend-The-Brushes-Editor)。  
  
### <a name="paint-a-repeating-image-or-pattern-on-an-object"></a>在对象上绘制重复图像或图案  
 可使用平铺画笔在对象上绘制重复图像或图案。  
  
 若要创建平铺画笔，请首先创建图像画笔、图形画笔或视觉画笔资源。  
  
 使用图像创建图像画笔。 下图显示图像画笔、平铺的图像画笔和翻转的图像画笔。  
  
 ![](../designers/media/81f84f56-906d-456b-8288-d77da1e01e31.png "81f84f56-906d-456b-8288-d77da1e01e31") ![](../designers/media/d3782ca8-64da-47a4-a095-c6cdd0fa47a2.png "d3782ca8-64da-47a4-a095-c6cdd0fa47a2") ![](../designers/media/38ae3691-f3f1-4a1e-82ca-c7fa164bf56e.png "38ae3691-f3f1-4a1e-82ca-c7fa164bf56e")  
  
 使用矢量图形（如路径或形状）创建图形画笔。 下图显示图形画笔、平铺的图形画笔和翻转的图形画笔。  
  
 ![](../designers/media/197666ac-ef57-4c5c-9779-669e991a00a5.png "197666ac-ef57-4c5c-9779-669e991a00a5") ![](../designers/media/ba09cda3-4cee-40ba-b3d4-edc032158bdc.png "ba09cda3-4cee-40ba-b3d4-edc032158bdc") ![](../designers/media/15bf6021-620c-4490-9eae-086153d3f14f.png "15bf6021-620c-4490-9eae-086153d3f14f")  
  
 通过控件（如按钮）创建视觉画笔。 下图显示视觉画笔和平铺的视觉画笔。  
  
 ![](../designers/media/fb6c90e0-153c-48fe-b563-e601beac6227.png "fb6c90e0-153c-48fe-b563-e601beac6227") ![](../designers/media/e261b99f-7d8f-4d91-bc84-19c7beccc255.png "e261b99f-7d8f-4d91-bc84-19c7beccc255")  
  
 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [平铺画笔](http://www.popscreen.com/v/6A4iM/Microsoft-Expression-Blend-Tile-Brushes)。  
  
## <a name="Styles"></a> 样式和模板：跨控件创建一致的外观  
 可以一次性设计控件的外观和行为，然后将该设计应用于其他控件，以便不必分别进行维护。  
  
 **是否应使用样式？**：如果只是想设置默认属性（如按钮的颜色），请使用样式。 即使在应用了样式之后，也可以修改控件。  
  
 **是否应使用模板？**：如果想要更改控件的结构，请使用模板。 假设将图形或徽标转换为按钮。 在向其应用模板之后，无法修改控件。  
  
### <a name="create-a-template-or-style"></a>创建模板或样式  
 可通过两种方法创建模板。 可以将美工板上的任何对象转换为控件，也可以使模板基于现有控件。  
  
 若要将任何对象转换为控件模板，请选择对象，然后在“工具”菜单上，选择“构成控件”。  
  
 如果想要使模板基于现有控件，请选择美工板上的对象。 然后，在美工板顶部，选择痕迹导航按钮，选择“编辑模板”，然后选择“编辑副本”或“创建空白项”。  
  
 ![](../designers/media/5ebdb33f-aad2-4c10-a328-5e8b04c56a36.png "5ebdb33f-aad2-4c10-a328-5e8b04c56a36")  
  
 若要创建样式，请选择对象，在“对象”菜单上选择“编辑样式”，然后选择“编辑副本”或“创建空白项”。  
  
- 选择“编辑副本”可从控件的默认样式或模板开始。  
  
- 选择“创建空白项”可从头开始。  
  
  仅当编辑已创建的样式或模板时，“编辑当前形状”选项才会出现。 对于仍在使用默认系统模板的控件，它不会出现。  
  
  在“创建样式资源”对话框中，可以命名样式或模板以便可以在以后使用它，也可以将样式或模板应用于该类型的所有控件。  
  
  ![](../designers/media/4818ee6a-ce60-4b79-91c8-3b1871829eea.png "4818ee6a-ce60-4b79-91c8-3b1871829eea")  
  
> [!NOTE]
> 不能为控件的每种类型都创建样式或模板。 如果控件不支持它们，则痕迹导航按钮不会出现在美工板上方。  
>   
> 若要返回主文档的编辑范围，请单击“返回范围”![](../designers/media/55844eb3-ed98-4f20-aa66-a6f5b23eeb2b.png "55844eb3-ed98-4f20-aa66-a6f5b23eeb2b")。  
>   
> ![](../designers/media/4a5612e1-7a28-4587-b870-0fe7112ec2ad.png "4a5612e1-7a28-4587-b870-0fe7112ec2ad")  
  
 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [创建样式](https://www.youtube.com/watch?v=W8YdXDPeKdc)。  
  
### <a name="apply-a-style-or-template-to-a-control"></a>将样式或模板应用于控件  
 在[对象和时间线](https://msdn.microsoft.com/135a5a5e-ec6d-4f38-8827-60e284cd5f57)面板中右键单击某个对象，选择“编辑模板”，然后选择“应用资源”。  
  
 ![](../designers/media/dc12debc-7711-47d9-84ce-10322a384397.png "dc12debc-7711-47d9-84ce-10322a384397")  
  
### <a name="restore-the-default-style-or-template-of-a-control"></a>还原控件的默认样式或模板  
 选择控件，在[属性面板](https://msdn.microsoft.com/135a5a5e-ec6d-4f38-8827-60e284cd5f57)中，找到“样式”或“模板”属性。 然后，单击“高级选项”![](../designers/media/12e06962-5d8a-480d-a837-e06b84c545bb.png "12e06962-5d8a-480d-a837-e06b84c545bb")，再在快捷菜单上单击“重置”。  
  
## <a name="Visual"></a> 可视状态：根据控件状态更改其外观  
 控件可以基于用户交互而具有不同的视觉外观。 例如，可以在用户单击时使按钮变为绿色，也可以运行动画。 可使用过渡缩短或延长可视状态之间的时间。  
  
 ![](../designers/media/a95c671a-5639-40b9-83db-1e6b214330d5.png "a95c671a-5639-40b9-83db-1e6b214330d5")  
  
 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [管理 WPF 控件的状态](https://www.youtube.com/watch?v=m0PlkF5i6uw)。  
  
## <a name="Resources"></a> 资源：创建颜色、样式和模板，并在以后重复使用它们  
 可以将项目中的几乎所有对象转换为资源。 资源只是可以在应用程序中的不同位置重复使用的对象。 例如，可以一次性创建一种颜色，使它成为资源，然后在多个对象上使用该颜色。 若要更改所有这些对象的颜色，只需更改该颜色资源。  
  
 ![](../designers/media/89203705-cf66-46e0-b153-52a23cd744f7.png "89203705-cf66-46e0-b153-52a23cd744f7") ![](../designers/media/6bff8b19-3cd5-41a0-bbf9-ff65532d5aae.png "6bff8b19-3cd5-41a0-bbf9-ff65532d5aae")  
  
 **观看短片：**![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [简要了解资源](http://www.popscreen.com/v/6A4k7/Microsoft-Expression-Blend-Brief-Touch-on-Resources)。  
  
## <a name="see-also"></a>请参阅  
 [使用 Blend for Visual Studio 创建 UI](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
