---
title: 标志标记 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.flag
ms.assetid: f3ec919e-63e5-484b-adbf-8f0e79342e75
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ccc0c7aa3386e906ad13331a596953db70240701
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62969930"
---
# <a name="flag-markers"></a>标志标记
标志标记表示某一瞬间在应用中发生的事。 标志可以表示许多应用程序事件。 例如，标志可以显示特定工作项的计划时间或引发异常的时间。 诸如任务并行库等运行时也可以生成标志。

## <a name="flag-importance"></a>标志重要性
 标志以不同的大小显示，具体取决于它们的重要性。 与所有标记一样，重要性可以是低、常规、高或重要。  此图按重要性级别显示各标记的外观：

 ![“低”、“正常”、“高”和“严重”重要性标记](../profiling/media/cvmarkerimportance.png "CVMarkerImportance") 显示标志重要性的标记

## <a name="flag-category"></a>标志类别
 标志显示为五种不同的颜色，具体取决于其类别。 如果有 5 个以上的类别，则会重复使用颜色。 不能选择颜色。 与所有标记一样，类别可以是任意整数。 下一个插图显示前 5 个类别的颜色。

 ![类别标记的 5 种颜色](../profiling/media/cvmarkercategory.png "CVMarkerCategory") 显示类别的标记

## <a name="alerts"></a>警报
 警报是一种表示重要应用程序事件（例如，异常）的红色标志。  以下是一个警报：

 ![并发可视化工具警报标记](../profiling/media/cvmarkeralert.png "CVMarkerAlert") 警报标记

## <a name="aggregation-flags"></a>聚合标志
 有时，并发可视化工具中标志的发生时间过于接近，导致无法单独绘制。 发生这种情况时，将显示代表基础标志的灰色聚合标志  。 当将鼠标指针放在这些图标上时，工具提示将显示所代表的基础标志数量。 若要查看这些标志，请将其放大。 如果一直放大但仍显示聚合标志，则可以在[标记报表](../profiling/markers-report.md)中查看基础标志。

 聚合标志以不同的大小绘制。 标志的大小取决于聚合中最重要的标志所具有的重要性级别。 下图按重要性从低到高显示聚合标志。

 ![聚合显示 4 个重要性级别的标志](../profiling/media/cvmarkeraggregate.png "CVMarkerAggregate") 不同重要性级别的聚合标志

## <a name="see-also"></a>请参阅
- [并发可视化工具标记](../profiling/concurrency-visualizer-markers.md)
- [并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md)