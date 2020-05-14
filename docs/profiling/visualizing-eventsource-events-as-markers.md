---
title: 将 EventSource 事件作为标记可视化 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3a10022a-5c37-48b1-a833-dd35902176b6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bd6339b3f55b4a4c9a1e2c90ff3183a36f16c178
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "64811551"
---
# <a name="visualize-eventsource-events-as-markers"></a>将 EventSource 事件作为标记可视化
并发可视化工具可以将 EventSource 事件显示为标记，并且可以控制标记的显示方式。 若要查看 EventSource 标记，请使用[高级设置](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md)对话框注册 ETW 提供程序 GUID。 并发可视化工具具有将 EventSource 事件表示为[标志标记](../profiling/flag-markers.md)、[范围标记](../profiling/span-markers.md)和[消息标记](../profiling/message-markers.md)的默认约定。 可以通过向事件添加自定义字段自定义 EventSource 事件的显示方式。 有关标记的详细信息，请参阅[并发可视化工具标记](../profiling/concurrency-visualizer-markers.md)。 有关 EventSource 事件的详细信息，请参阅 <xref:System.Diagnostics.Tracing>。

## <a name="default-visualization-of-eventsource-events"></a>EventSource 事件的默认可视化效果
 默认情况下，并发可视化工具使用以下约定来表示 EventSource 事件。

### <a name="marker-type"></a>标记类型

1. 具有[操作码](/windows/desktop/WES/eventmanifestschema-opcodetype-complextype) win:Start 或 win:Stop 的事件将分别被视为范围的开始或结束。  无法显示嵌套或重叠的范围。 无法显示以一个线程开始并以另一个线程结束的事件对。

2. 其操作码既不是 win:Start 也不是 win:Stop 的事件将被视为标记标志，除非其[级别](/windows/desktop/WES/defining-severity-levels)（EVENT_RECORD.EVENT_HEADER.EVENT_DESCRIPTOR 的字段）为 win:Verbose 或更高版本。

3. 在所有其他情况下，事件均被视为消息。

### <a name="importance"></a>Importance
 下表定义了事件级别映射到标记重要性的方式。

|ETW 级别|并发可视化工具重要性|
|---------------|---------------------------------------|
|win:LogAlways|一般|
|win:Critical|严重|
|win:Error|严重|
|win:Warning|高|
|win:Informational|一般|
|win:Verbose|低|
|大于 win:verbose|低|

### <a name="series-name"></a>序列名称
 事件的任务名称用于序列名称。 如果未为该事件定义任何任务，则序列名称为空。

### <a name="category"></a>类别
 如果级别为 win:Critical 或 win:Error，则类别为警报 (-1)。 否则，类别为默认值 (0)。

### <a name="text"></a>文本
 如果为事件定义了 printf 类型的格式化文本消息，它将显示为标记的说明。 否则，说明则是该事件的名称和每个负载字段的值。

## <a name="customize-visualization-of-eventsource-events"></a>EventSource 事件的自定义可视化效果
 如以下各节中所述，可以通过向事件添加合适的字段来自定义 EventSource 事件的显示方式。

### <a name="marker-type"></a>标记类型
 使用 `cvType` 字段（一个字节）控制用于表示该事件的标记种类。 以下是可用于 cvType 的值：

|cvType 值|生成的标记类型|
|------------------|---------------------------|
|0|消息|
|1|范围开始|
|2|范围结束|
|3|Flag|
|所有其他值|消息|

### <a name="importance"></a>Importance
 可以使用 `cvImportance` 字段（一个字节）控制 EventSource 事件的重要性设置。 但是，我们建议通过使用其级别来控制事件显示的重要性。

|cvImportance 值|并发可视化工具重要性|
|------------------------|---------------------------------------|
|0|一般|
|1|严重|
|2|高|
|3|高|
|4|一般|
|5|低|
|所有其他值|低|

### <a name="series-name"></a>序列名称
 使用 `cvSeries` 事件字段（一个字符串）控制并发可视化工具给予 EventSource 事件的序列名称。

### <a name="category"></a>类别
 使用 `cvCategory` 字段（一个字节）控制并发可视化工具给予 EventSource 事件的类别。

### <a name="text"></a>文本
 使用 `cvTextW` 字段（一个字符串）控制并发可视化工具给予 EventSource 事件的说明。

### <a name="spanid"></a>SpanID
 使用 cvSpanId 字段（一个整数型）匹配事件对。 每对开始/停止事件的值，该值表示范围必须是唯一的。 通常对于并发代码，这需要使用同步基元（如 <xref:System.Threading.Interlocked.Exchange%2A>）以确保密钥（用于 CvSpanID 的值）正确。

> [!NOTE]
> 不支持以下操作：使用 SpanID 以嵌套范围，允许它们部分重叠在同一线程上或允许它们以一个线程开始并以另一个线程结束。

## <a name="see-also"></a>另请参阅
- [并发可视化工具标记](../profiling/concurrency-visualizer-markers.md)