---
title: 在 XAML 设计器中动态显示对象 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: fb88fa26-e835-47f5-9771-2f279441c83c
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ea2fdf1f47385a9be26fa65a93b9104b2d864079
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658024"
---
# <a name="animate-objects-in-xaml-designer"></a>在 XAML 设计器中动态显示对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以创建移动对象或使它们淡入和淡出的简短动画。

 若要开始，请创建 *情节提要*。 情节提要包含一个或多个 *时间线*。 在时间线上设置 *关键帧* 以标记属性更改。 随后在运行动画时，Blend 将在指定时间段内插入属性更改。 这样便可实现平滑过渡。 可以对属于对象的任何属性（甚至非可视属性）进行动画处理。

 下图显示了一个名为“MoveUp”的情节提要。 时间线包含标记矩形的 X 和 Y 位置的关键帧。 当此动画运行时，矩形平滑地从一个位置移动到另一个位置。

 ![](../designers/media/982f031a-74a3-414a-abc2-a0f41a741075.png "982f031a-74a3-414a-abc2-a0f41a741075")

 通过观看这些视频了解如何创建动画。

|观看简短视频：|了解如何：|
|--------------------------|-------------------|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[创建时间线](http://www.popscreen.com/v/6A4eF/Microsoft-Expression-Blend-Creating-Timelines)|创建时间线，以及在时间线中使用对象。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[添加关键帧和重复动画](http://www.popscreen.com/v/6A4fi/Microsoft-Expression-Blend-Adding-Keyframes-and-Repeating-an-Animation)|添加关键帧，并在每个关键帧处设置属性。 随后运行动画并观看对象在它们之间平滑过渡。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[添加事件触发器以实现交互性](http://www.popscreen.com/v/6A4e4/Microsoft-Expression-Blend-Adding-Event-Triggers-for-Interactivity)|在事件发生时启动动画。 例如，在窗口加载时启动一个动画。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[动画颜色](http://www.popscreen.com/v/6A4gv/Microsoft-Expression-Blend-Animating-Colors)|使用动画更改对象的颜色。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[创建和修改运动路径](http://www.popscreen.com/v/6A4fX/Microsoft-Expression-Blend-Creating-and-Modifying-Motion-Paths)|沿着路径对对象进行动画处理。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[缓动关键帧](http://www.popscreen.com/v/6A4dM/Microsoft-Expression-Blend-Easing-Keyframes)|在接近开头（*缓动进入*）或接近末尾（*缓动退出*）处加快或减慢动画。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[对按钮进行动画处理](http://www.popscreen.com/v/6A4fK/Microsoft-Expression-Blend-Animating-a-Button)|创建在用户指向按钮时出现在按钮上的有趣效果。|
|![配置已安装的功能](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon")[创建动画和使用缓动](https://www.youtube.com/watch?v=mAJXYrwxGYo)|当用户按下计算器图像上的按钮时出现的动画效果。|

## <a name="see-also"></a>请参阅
 [使用 Blend for Visual Studio 创建 UI](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
