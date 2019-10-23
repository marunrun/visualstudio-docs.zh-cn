---
title: 放大负载测试结果关系图
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.monitor.graphzoom
helpviewer_keywords:
- graphs, analyzing load tests
- load tests, zooming with graphs
ms.assetid: 729b4c30-4bc3-4698-91b3-17a676897443
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f8e37d7ce5f4f52074904aa353ad6d02d65f5ca6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653261"
---
# <a name="how-to-zoom-in-on-a-region-of-the-graph-in-load-test-results"></a>如何：放大负载测试结果中关系图的区域

完成负载测试后，可使用缩放条来放大并滚动到关系图的某一区域。 通过放大，可以更细致地检查在负载测试运行过程中所生成的数据。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

放大功能仅在分析已完成的负载测试的结果时才可用，而在观察正在运行的测试的结果时不可用。

仅当在缩放模式下查看负载测试结果时，缩放控件才在负载测试分析器中显示  。 在负载测试已完成或加载了以前运行的负载测试时，会在关系图视图中建立缩放模式。 可以使用工具栏上的“显示缩放控件”来显示或隐藏关系图上的缩放控件  。

可以调整“水平 x 轴缩放”以分析负载测试过程中的特定时间段  。 可以调整“垂直 y 轴缩放”以分析关系图中包含的计数器的特定值范围  。

可以使用鼠标来调整“水平时间线”和“垂直值范围”缩放控件   。 也可以使用向左键和向右键来调整“水平时间线控件”  。 通过使用箭头键调整缩放控件，可以按每次 1 个采样间隔来调整窗口范围。 使用 Shift 和箭头键，可以按 10 个采样间隔来进行调整  。

要使用箭头键调整缩放控件，首需先通过 Tab 键设置缩放控件的焦点  。 当焦点在左滑块上时，箭头键会按 1 个间隔向左或向右移动缩放窗口的起始边界。 当焦点在中心滑块上时，可以使用箭头键将缩放窗口向左或向右滚动 1 个采样间隔，而不更改缩放窗口的大小。 最后，右滑块移动，将缩放窗口的结束范围扩大或缩小 1 个采样间隔。

若要将水平和垂直缩放控件恢复为显示完整时间线和值范围，可以使用关系图上的弹出菜单中的“水平缩小”选项、“垂直缩小”选项或“在两个方向上均缩小”选项    。

> [!TIP]
> 可以使用工具栏中的“同步水平缩放控件”打开或关闭自动水平缩放同步  。 当同步打开时，应用于关系图的任何缩放也会应用于关系图视图上的任何其他关系图。

![图形视图缩放控件](../test/media/ltest_zoomcontrol.png)

在上图中，“受测系统”关系图已放大，以便调查阈值问题  。 已通过使用工具栏上“关系图选项”下拉列表中的“在关系图上显示阈值冲突”启用阈值冲突   。

有关详细信息，请参阅[在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)。

## <a name="display-graphs"></a>显示关系图

在通过放大或缩小或通过滚动来更改关系图的显示之前，请遵循此过程来显示关系图。

显示关系图：

1. 运行负载测试直到完成。

2. 当负载测试运行结束时，在询问是否查看负载测试结果存储区中的结果的对话框中，选择“是”  。

     \- 或 -

     查看上一次运行的负载测试的详细信息。 有关详细信息，请参阅[如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)。

3. 如果未显示关系图，请选择“关系图”  。

4. 如果未显示缩放条，请选择“显示缩放控件”  。

     每个关系图有两个缩放条可用。 控制垂直比例的缩放条出现在关系图的左侧。 控制水平比例的缩放条出现在关系图的下方。

     每个缩放条具有两个控点。 控点是位于缩放条每一端的矩形区域。

## <a name="zoom-and-scroll"></a>缩放和滚动

当显示多个关系图时，可以使它们保持同步，以便它们显示负载测试运行的相同部分。

### <a name="to-synchronize-zooming-and-scrolling"></a>同步缩放和滚动

1. 在负载测试分析器上，选择“同步水平缩放控件”   。

     当选中“同步水平缩放控件”按钮时，缩放和滚动单个关系图的时间比例的同时也将缩放和滚动其他关系图的时间比例  。

2. 再次选择“同步水平缩放控件”  。

     当未选择“同步水平缩放控件”按钮时，缩放和滚动单个关系图的时间比例只影响该关系图  。

### <a name="to-zoom-and-scroll-to-a-region-of-the-graph"></a>放大并滚动到关系图的区域

1. 在关系图下方的缩放条上，向右拖动左侧控点。

     这将放大测试运行的后面部分。 类似地，向左拖动右侧控点将放大测试运行的前面部分。

2. 若要放大某个特定区域，请将两个控点向关系图的中心滑动。

     两个控点之间的距离越近，放大程度就越高，以便显示负载测试更短、更精细的片段。

     选择缩放条的中心部分，然后拖动它以滚动到负载测试中的特定点。

### <a name="to-zoom-to-a-region-of-the-graph-by-choosing-and-dragging"></a>通过选择和拖动来缩放关系图的区域

1. 在缩放区域的一端选择关系图。

2. 将鼠标指针拖动到缩放区域的另一端。

3. 释放鼠标按钮。

    这将放大您通过选择和拖动定义的区域。

   下列过程描述如何快速进行缩小，而不必调整缩放条的两端。

### <a name="to-zoom-out"></a>缩小

1. 右击放大的关系图。

2. 从快捷菜单中选择“水平缩小”  。

     这将缩小以显示负载测试运行的整个持续时间。

## <a name="see-also"></a>请参阅

- [在关系图视图中分析负载测试结果](../test/analyze-load-test-results-in-the-graphs-view.md)
- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [如何：在关系图上添加和删除计数器](../test/how-to-add-and-delete-counters-on-graphs-in-load-test-results.md)