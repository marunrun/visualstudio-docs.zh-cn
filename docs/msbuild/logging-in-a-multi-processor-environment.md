---
title: 多处理器环境下的日志记录 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, multi-processor logging
- MSBuild, logging
ms.assetid: dd4dae65-ed04-4883-b48d-59bcb891c4dc
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0c332fb67e96bdfea0059de11441da7c32871633
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633559"
---
# <a name="logging-in-a-multi-processor-environment"></a>多处理器环境下的日志记录

MSBuild 使用多个处理器的能力可以显著缩短项目生成时间，但同时会增加日志记录的复杂性。 在单处理器环境下，记录器可以用可预测的顺序方式处理传入的事件、消息、警告和错误。 但在多处理器环境下，来自多个源的事件可能同时到达或以无序方式到达。 MSBuild 提供了可以识别多处理器的新记录器，并允许创建自定义“转发记录器”。

## <a name="log-multiple-processor-builds"></a>日志记录多处理器生成

在多处理器或多核系统中生成一个或多个项目时，MSBuild 将同时生成所有项目的生成事件。 大量事件数据可能会同时或以无序方式到达记录器。 这会严重影响记录器，并可能导致生成时间延长和记录器输出错误，甚至会导致生成中断。 为了解决这些问题，MSBuild 记录器可以处理无序事件，并将事件与其源建立关联。

通过创建自定义转发记录器，可以进一步提高日志记录效率。 自定义转发记录器可充当筛选器，生成前你只需选择要监视的事件。 使用自定义转发记录器时，不需要的事件不会严重影响记录器，造成日志混乱或降低生成速度。

### <a name="central-logging-model"></a>集中式日志记录模型

对于多处理器生成，MSBuild 使用“集中式日志记录模型”。 在集中式日志记录模型中，MSBuild.exe 的实例充当主生成进程或“中心节点”  。 MSBuild.exe 的辅助实例或者“辅助节点”会附加到中心节点  。 附加到中心节点的任何基于 ILogger 的记录器均称为“中心记录器”，附加到辅助节点的记录器均称为“辅助记录器”。

进行生成时，辅助记录器会将其事件流量路由到中心记录器。 由于事件来源于多个辅助节点，因此数据会同时但交错地到达中心节点。 为了解析事件到项目和事件到目标的引用，事件参数将包括其他生成事件上下文信息。

虽然只要求中心记录器实现 <xref:Microsoft.Build.Framework.ILogger>，但如果需要中心记录器使用参与生成的节点数进行初始化，则建议还要实现 <xref:Microsoft.Build.Framework.INodeLogger>。 引擎初始化记录器时，会调用 <xref:Microsoft.Build.Framework.ILogger.Initialize%2A> 方法的以下重载：

```csharp
public interface INodeLogger: ILogger
{
    public void Initialize(IEventSource eventSource, int nodeCount);
}
```

### <a name="distributed-logging-model"></a>分布式日志记录模型

在集中式日志记录模型中，有时会存在过多的传入消息流量，例如在一次性生成很多项目时，过多流量会严重影响中心节点，给系统带来压力，并降低生成性能。

为缓解这个问题，MSBuild 还启用了“分布式日志记录模型”，通过允许创建转发记录器，该模型扩展了集中式日志记录模型。 转发记录器会附加到辅助节点，并从该节点接收传入的生成事件。 转发记录器与常规记录器类似，只不过它可以筛选事件，然后只将所需事件转发到中心节点。 这样可以减少中心节点上的消息流量，提高性能。

 通过实现派生自 <xref:Microsoft.Build.Framework.ILogger> 的 <xref:Microsoft.Build.Framework.IForwardingLogger> 接口，可以创建转发记录器。 接口定义如下：

```csharp
public interface IForwardingLogger: INodeLogger
{
    public IEventRedirector EventRedirector { get; set; }
    public int NodeId { get; set; }
}
```

要转发转发记录器中的事件，请调用 <xref:Microsoft.Build.Framework.IEventRedirector> 接口 <xref:Microsoft.Build.Framework.IEventRedirector.ForwardEvent%2A> 方法。 以参数的形式传递相应的 <xref:Microsoft.Build.Framework.BuildEventArgs> 或派生类。

有关详细信息，请参阅[创建转发记录器](../msbuild/creating-forwarding-loggers.md)。

### <a name="attaching-a-distributed-logger"></a>附加分布式记录器

要在命令行生成上附加一个分布式记录器，请使用 `-distributedlogger`（或简称为 `-dl`）开关。 用于指定记录器类型名称和类名的格式与 `-logger` 开关对应的格式相同，只是分布式记录器由以下两个日志记录类组成：转发记录器和中心记录器。 以下是附加分布式记录器的示例：

```cmd
msbuild.exe *.proj -distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,
Culture=neutral*XMLForwardingLogger,MyLogger,Version=1.0.2,
Culture=neutral
```

用星号 (*) 来分隔 `-dl` 开关中的两个记录器名称。

## <a name="see-also"></a>另请参阅

- [生成记录器](../msbuild/build-loggers.md)
- [创建转发记录器](../msbuild/creating-forwarding-loggers.md)
