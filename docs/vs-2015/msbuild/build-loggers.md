---
title: 生成记录器 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing loggers
- MSBuild, logging
- logging [MSBuild]
ms.assetid: fa34810d-185a-4d22-92bd-9852915e5f1d
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2908c8217070196de1b2d3cd4f1c5f8d8f2868a5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160431"
---
# <a name="build-loggers"></a>生成记录器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

记录器提供一种方法，通过此方法可自定义生成的输出并显示消息、错误或警告以响应特定生成事件。 每个记录器作为 .NET 类实现，此类实现 Microsoft.Build.Framework.dll 程序集中定义的 <xref:Microsoft.Build.Framework.ILogger> 接口。  
  
 在实现记录器时，有两种方法可供选择：  
  
- 直接实现 <xref:Microsoft.Build.Framework.ILogger> 接口。  
  
- 从 Microsoft.Build.Utilities.dll 程序集中定义的帮助程序类 <xref:Microsoft.Build.Utilities.Logger> 中派生类。 <xref:Microsoft.Build.Utilities.Logger> 实现 <xref:Microsoft.Build.Framework.ILogger>，并提供了一些 <xref:Microsoft.Build.Framework.ILogger> 成员的默认实现代码。  
  
  本主题将介绍如何编写派生自 <xref:Microsoft.Build.Utilities.Logger> 的简单记录器，并在控制台上显示用于响应特定生成事件的消息。  
  
## <a name="registering-for-events"></a>注册事件  
 记录器的目的是收集有关生成进度的信息（正如生成引擎所报告的信息），随后以有用的方式报告该信息。 所有记录器都必须重写 <xref:Microsoft.Build.Utilities.Logger.Initialize%2A> 方法，即记录器用于注册事件的位置。 在此示例中，记录器注册 <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>、<xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> 和 <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> 事件。  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#2](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#2)]  
  
## <a name="responding-to-events"></a>对事件作出响应  
 记录器注册特定事件后，这些事件出现时，记录器需要处理这些事件。 对于 <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> 和 <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished> 事件，记录器只写入一个短语，以及事件涉及的项目文件的名称。 记录器中的所有消息都写入到控制台窗口。  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#3](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#3)]  
  
## <a name="responding-to-logger-verbosity-values"></a>响应记录器详细信息值  
 在某些情况下，如果 MSBuild.exe **/verbosity** 开关包含特定值，可能需要仅记录事件中的信息。 在此示例中，如果 <xref:Microsoft.Build.Utilities.Logger.Verbosity%2A> 属性为 <xref:Microsoft.Build.Framework.LoggerVerbosity>`Detailed`（由 /verbosity  开关设置），<xref:Microsoft.Build.Framework.IEventSource.TargetStarted> 事件处理程序仅记录一条消息。  
  
 [!code-csharp[msbuild_SimpleConsoleLogger#4](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#4)]  
  
## <a name="specifying-a-logger"></a>指定记录器  
 将记录器编译到程序集后，你需要告诉 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 在生成过程中使用该记录器。 可以通过配合使用 **/logger** 开关和 MSBuild.exe 来执行此操作。 有关可用于 MSBuild.exe 的开关的详细信息，请参阅[命令行引用](../msbuild/msbuild-command-line-reference.md)。  
  
 以下命令行生成项目 `MyProject.csproj`，并使用在 `SimpleLogger.dll` 中实现的记录器类。 **/nologo** 开关隐藏版权标志和版权消息， **/noconsolelogger** 开关禁用默认的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 控制台记录器。  
  
```  
MSBuild /nologo /noconsolelogger /logger:SimpleLogger.dll  
```  
  
 以下命令行通过相同记录器生成项目，但是 `Verbosity` 级别为 `Detailed`。  
  
```  
MSBuild /nologo /noconsolelogger /logger:SimpleLogger.dll /verbosity:Detailed  
```  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 下面的示例包含记录器的完整代码。  
  
### <a name="code"></a>代码  
 [!code-csharp[msbuild_SimpleConsoleLogger#1](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleConsoleLogger/CS/msbuild_SimpleConsoleLogger.cs#1)]  
  
### <a name="comments"></a>注释  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 以下示例演示如何实现将日志写入到文件的记录器（而非在控制台窗口中显示记录器）。  
  
### <a name="code"></a>代码  
 [!code-csharp[msbuild_BasicLogger#1](../snippets/csharp/VS_Snippets_Misc/msbuild_BasicLogger/CS/msbuild_BasicLogger.cs#1)]  
  
### <a name="comments"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)   
 [MSBuild 概念](../msbuild/msbuild-concepts.md)
