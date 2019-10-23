---
title: 使用关系图视图图例分析负载测试
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Load Test Analyzer, graphs view legend
- load tests, graphs view legend
ms.assetid: 0f6ba8e4-1343-419c-8a9f-240cf50efed7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 17f91ba90a6a9de1c4084d4186adae6ab8388f23
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659830"
---
# <a name="use-the-graphs-view-legend-to-analyze-load-tests"></a>使用关系图视图图例分析负载测试

负载测试分析器的关系图视图包含一个图例面板，用于显示与当前选择的关系图关联的每个性能计数器的信息。

![图形视图图例](../test/media/load_viewlegend.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

图例中包含以下信息：

- **在关系图上显示：** 使用这些复选框，可指定是否在关系图上绘制特定计数器（如“User load”或“Errors/Sec”）的线条   。 如果要在关系图上绘制线条，则选中一个复选框。 清除复选框可从关系图中移除绘图线条。 在移除绘制线条时，计数器的统计信息会继续显示在图例中。

- **范围：** 此列显示性能计数器的 y 轴范围。 默认情况下，此值会随着样本数据范围的更改而自动调整。 自动调整的范围始终为大于最大值的下一个 10 的幂；这包括 10 的负数幂。 关系图可以包含各种计数器，其中每个计数器都有不同的范围。 因此，y 轴不会用任何特定范围进行标记，而是用 0-100 之间的值进行标记，这些值表示每个计数器的总体范围百分比。 例如，对于范围为 1000 的计数器，y 轴上的数据点 60 将对应于该计数器的值 600。

    > [!NOTE]
    > 可以通过将范围锁定为特定值来关闭自动范围值调整。 当范围锁定后，超过该范围的任何值都会在关系图顶部显示为指定的最大值。 使用“绘图选项”对话框可将范围锁定为特定值  。

- **计数器：** 四个分别名为“计数器”、“实例”、“类别”和“计算机”的列一起唯一地标识性能计数器     。

- **颜色：** “颜色”列显示性能计数器的绘制线条的颜色和线型  。 使用“绘图选项”对话框，可以更改关系图上性能计数器的颜色或线型  。 可以从图例的快捷菜单访问“绘图选项”对话框  。

- **统计信息：** “最小”、“最大”、“平均”和“最新”列数显示了性能计数器的相应统计信息     。 这些值对应于在关系图的可见区域上显示的数据。 例如，如果放大运行的某个区域，则图例统计信息将仅反映缩放区域的值。 “最后一个”列是性能计数器针对最近完成的采样间隔的值。

    > [!NOTE]
    > 当负载测试正在运行时，“最后一个”列才会显示在负载测试分析器的图例中。

     有关详细信息，请参阅[如何：放大关系图的区域](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)。

在图例中选择某一项可实现以下操作：

- 允许从图例和关系图中移除该项。 右键单击项目并选择“删除”，或者按“删除”键   。

- 在关系图上突出显示绘制线条。

- 让数据网格显示所选项的数据。

- 使你能够访问计数器的“绘图选项”对话框  。

> [!TIP]
> 可以使用负载测试分析器工具栏中的“关系图选项下拉列表”按钮，然后选择“显示图例”以显示或隐藏与关系图视图关联的“图例”面板     。

## <a name="see-also"></a>请参阅

- [如何：放大关系图的区域](../test/how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results.md)
- [在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)
