---
title: 在 XAML 设计器中动态显示对象
titleSuffix: Blend for Visual Studio
ms.date: 07/31/2019
ms.topic: conceptual
ms.assetid: fb88fa26-e835-47f5-9771-2f279441c83c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4b396c0428f9810fe41fa70aca7b52fba2dd4f5b
ms.sourcegitcommit: 90c3187d804ad7544367829d07ed4b47d3f8a72d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68822165"
---
# <a name="animate-objects-in-xaml-designer"></a>在 XAML 设计器中动态显示对象

通过 Blend for Visual Studio 可以轻松地创建移动对象或使它们淡入淡出等的简短动画。

若要创建动画，你需要情节提要  。 情节提要包含一个或多个 *时间线*。 在时间线上设置 *关键帧* 以标记属性更改。 随后在运行动画时，Blend for Visual Studio 将在指定时间段内插入属性更改。 这样便可实现平滑过渡。 可以对属于对象的任何属性（甚至非可视属性）进行动画处理。

下图显示了一个名为“Storyboard1”  的情节提要。 时间线包含标记矩形的 X 和 Y 位置的关键帧。 当此动画运行时，矩形平滑地从一个位置移动到另一个位置。

![Blend for Visual Studio 中的动画的情节提要](../designers/media/storyboard-timeline.png)

## <a name="create-an-animation"></a>创建动画

1. 若要创建情节提要，请在“对象和时间线”窗口中选择“情节提要选项”按钮，然后选择“新建”    。

   ![在 Blend for Visual Studio 中添加情节提要](media/new-storyboard.png)

2. 在“创建情节提要资源”对话框中，输入情节提要的名称  。

3. 在设计视图的“资产”面板中，将一个矩形添加到页面的左下角  。

   ![XAML 设计器的“资产”面板中的矩形](media/add-rectangle.PNG)

4. 在“对象和时间线”窗口中，将黄色时间指针移动到 3 秒处   。

   ![时间线中的时间指示器](media/timeline-indicator.PNG)

5. 在页面的设计视图中，将矩形拖到页面的右侧。

6. 按“播放”，观看矩形从页面左侧移动到页面右侧  。

在不同的时间点对矩形进行其他更改。 例如，可以在“属性”窗口中更改填充颜色或翻转方向。

## <a name="see-also"></a>请参阅

- [使用 Blend for Visual Studio 创建 UI](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)