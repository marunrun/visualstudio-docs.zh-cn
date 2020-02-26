---
title: 创建转发记录器 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, forwarding loggers
- MSBuild, logging
ms.assetid: 3aebf9c8-b62c-4cb2-b2d6-8cdfcd369a24
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 76dd68749fc38a53daa91269ecebfdb4c53b706e
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578779"
---
# <a name="create-forwarding-loggers"></a>创建转发记录器
在多处理器系统上生成项目时，转发记录器允许选择要监视的事件，提高了日志记录效率。 启用转发记录器后，可防止不必要的事件影响中心记录器、降低生成速度以及造成日志混乱。

 要创建转发记录器，可实现 <xref:Microsoft.Build.Framework.IForwardingLogger> 接口，然后手动实现其方法，或者使用 <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> 类及其预配置的方法。 （后者可满足大多数应用程序。）

## <a name="register-events-and-respond-to-them"></a>注册并响应事件
 辅助生成引擎报告生成事件后，转发记录器会收集有关生成事件的信息，这是主生成过程在多处理器系统上进行生成的过程中创建的工作进程。 然后转发记录器会根据你提供的说明，选择要转发到中心记录器的事件。

 必须注册转发记录器，才能处理要监视的事件。 要注册事件，记录器必须重写 <xref:Microsoft.Build.Utilities.Logger.Initialize%2A> 方法。 此方法现包含一个可选参数 `nodecount`，该参数可设置为系统中处理器的数目。 （该值默认为 1。）

 可监视事件的示例包括 <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> 和 <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished>。

 在多处理器环境中，事件消息的接收顺序可能是紊乱的。 因此，必须使用转发记录器中的事件处理程序评估事件，并对其进行编程，才能确定将哪些事件传递给重定向程序以转发到中心记录器。 为此，可使用附加到每条消息上的 <xref:Microsoft.Build.Framework.BuildEventContext> 类来协助标识要转发的事件，然后将事件名称传递给 <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> 类（或其子类）。 在使用此方法时，无需要其他特定的编码即可转发事件。

## <a name="specify-a-forwarding-logger"></a>指定转发记录器
 转发记录器编译为程序集后，必须告知 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 在生成过程中使用该程序集。 为此，请使用 `-FileLogger`、`-FileLoggerParameters` 和 `-DistributedFileLogger` 开关，以及 MSBuild.exe  。 `-FileLogger` 开关会告知 MSBuild.exe 已直接附加记录器  。 `-DistributedFileLogger` 开关表示每个节点都存在一个日志文件。 要在转发记录器上设置参数，请使用 `-FileLoggerParameters` 开关。 有关以上开关和其他 MSBuild.exe 开关的详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)  。

## <a name="multi-processor-aware-loggers"></a>可识别多处理器的记录器
 在多处理器系统上生成项目时，来自每个处理器的生成消息并不会按统一的顺序自动交错。 因此，必须使用附加到每条消息上的 <xref:Microsoft.Build.Framework.BuildEventContext> 类建立消息分组优先级。 有关多处理器生成的详细信息，请参阅[多处理器环境下的日志记录](../msbuild/logging-in-a-multi-processor-environment.md)。

## <a name="see-also"></a>请参阅
- [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)
- [生成记录器](../msbuild/build-loggers.md)
- [多处理器环境下的日志记录](../msbuild/logging-in-a-multi-processor-environment.md)