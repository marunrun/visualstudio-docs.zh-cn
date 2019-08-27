---
title: 调试 - 数据可视化效果
description: 调试是编程中常见且必要的部分。 Visual Studio for Mac 提供了一整套易于调试的功能。 本文介绍在调试程序中检查对象时可以查看的各种数据可视化效果。
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.technology: vs-ide-debug
ms.assetid: 527E6BEC-EF15-4002-ACB5-62AE1C16F6B7
ms.openlocfilehash: 0b9ec63855eff0b69f5523b1905b79d360509e67
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62932175"
---
# <a name="data-visualizations"></a>数据可视化效果

Visual Studio for Mac 提供调试程序用户界面支持，允许调试时的变量、字段或属性的值的可视化效果。 这些数据可视化工具显示数据的扩展版本，使开发者可以检查已知结构，例如显示颜色结构的颜色。

用户将鼠标悬停在行上时，单击值右侧的预览图标，可显示调试“本地”面板中的可视化工具：

![“本地”面板](media/data-visualizations-image9.png)

下表显示了在 Visual Studio for Mac 中调试时多个可用的新可视化效果。

## <a name="point"></a>点
iOS 和 Mac 中的 Point/PointF 或 CGPoint 作为元组呈现，在调试面板中显示 X 和 Y 值：

![点可视化效果](media/data-visualizations-image10.png)

## <a name="size"></a>大小
iOS 和 Mac 中的 Size/SizeF 或 CGSize 作为矩形呈现。 其按比例绘制，直到某一维度增长超过 250 像素，此时将按最大维度为 250 像素来缩放矩形：

[大小可视化](media/data-visualizations-image11.png)

## <a name="rectangle"></a>矩形
iOS 和 Mac 中的 Rectangle/RectangleF 或 CGRect 显示维度和原点。 与大小类似，它也按比例绘制，直到某一维度增长超过 250 像素：

![矩形可视化效果](media/data-visualizations-image12.png)

## <a name="coordinate"></a>坐标
坐标绘制在地图上，位置固定在中心：

[坐标可视化](media/data-visualizations-image13.png)

## <a name="color"></a>颜色
这将显示 UIColor、CGColor 和 Color 属性，描述颜色预览、RGBA 组件、“色调-饱和度-光”值和颜色的十六进制值：

![颜色可视化效果](media/data-visualizations-image14.png)

## <a name="images"></a>图像

媒体将按比例呈现（最大维度为 250 像素），且当图像超过 250 像素时，将缩放到合适比例：

![图像可视化效果](media/data-visualizations-image15.png)

## <a name="bezier-curves"></a>贝塞尔曲线

可视化工具将显示 `NSBezierPath`：

![贝塞尔曲线可视化效果](media/data-visualizations-image16.png)

## <a name="string"></a>String

少于 100 个字符的字符串会完整显示，没有预览。 更长的字符串在预览中完整显示。 字符串可编辑，可视化工具有一个编辑按钮，可在预览或在字符串值编辑器中编辑字符串值，如下所示：

![字符串可视化效果](media/data-visualizations-image17.png)

### <a name="small-strings"></a>小字符串：
![小字符串可视化效果](media/data-visualizations-image18.png)]

### <a name="medium-length-strings"></a>中等长度字符串：
![中等长度字符串可视化效果](media/data-visualizations-image19.png)

### <a name="editor"></a>编辑器：

![编辑器可视化效果](media/data-visualizations-image21.png)

## <a name="ienumerable"></a>IEnumerable

IEnumerable 枚举所有值，可单击“显示”值按钮查看每个值。 IEnumerable 选项不会显示 `Array`、`ArrayList`、`List<>`、`Dictionary<,>` 等对象的值，因为它们有自己的调试程序可视化工具。

![IEnumerable 可视化效果](media/data-visualizations-image22.png)

## <a name="other-visualizers"></a>其他可视化工具

下面列出了其他一些也有自己内联的可视化工具的类型：

![其他可视化效果](media/data-visualizations-image23.png)

* **基元**
  * 这将显示基元类型的原始值。
* **Enum**
  * 这将显示字段值，不含枚举类型限定符。
* **Tuple**
  * 以 (,) 的格式显示
* **Null**
  * 显示“null”值。
* **URL**
  * 这将显示一个可点击的超链接。
* **IntPtr**
  * 这将显示 IntPtr 的十六进制表示形式。

## <a name="see-also"></a>请参阅

- [检查“自动”窗口和“局部变量”窗口中的变量（Windows 上的 Visual Studio）](/visualstudio/debugger/autos-and-locals-windows)
- [查看可视化工具中的字符串（Windows 上的 Visual Studio）](/visualstudio/debugger/string-visualizer-dialog-box)