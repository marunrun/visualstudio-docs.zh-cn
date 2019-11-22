---
title: IntelliTrace Features | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- IntelliTrace, debugging with events
- IntelliTrace, recording execution history
- debugging [Visual Studio ALM], recording execution history
- IntelliTrace, turn off
- IntelliTrace, navigating event and call history
- IntelliTrace, saving your session
- IntelliTrace, enabling
- IntelliTrace, start debugging
- IntelliTrace, debugging with events and call information
- IntelliTrace, disabling
- IntelliTrace, turn on
- debugging [Visual Studio ALM], IntelliTrace
ms.assetid: 5ccc059c-6097-46b4-9d4b-34236c02d549
caps.latest.revision: 73
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dc16094c98a912d073bd6b873ecb3d1b3b411d1e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298953"
---
# <a name="intellitrace-features"></a>IntelliTrace 功能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用 IntelliTrace 记录事件和调用应用程序的方法，它让你能够在执行中的不同位置检查其状态（调用堆栈和局部变量值）。 Just start debugging as usual - IntelliTrace is turned on by default, and you can see the information IntelliTrace is recording in the new **Diagnostic Tools** window under the **Events** tab. Select an event and click **Activate Historical Debugging** to see the call stack and locals recorded for this event.  
  
 有关分步说明，请参阅[演练：使用 IntelliTrace](../debugger/walkthrough-using-intellitrace.md)。  
  
 Visual Studio Enterprise 版中提供 IntelliTrace，但 Visual Studio Professional 或 Community 版中不提供。  
  
 To confirm that IntelliTrace is turned on, open the **Tools / Options / IntelliTrace** options page. 默认情况下应选中“启用 IntelliTrace”。  
  
> [!NOTE]
> “IntelliTrace”选项页上的所有设置都针对 Visual Studio 这个整体，而不针对单个项目或解决方案。 这些设置中的更改适用于 Visual Studio 的所有实例、所有调试会话和所有项目或解决方案。  
  
## <a name="ChooseEvents"></a> Choose the events that IntelliTrace records  
 可以启用或禁用针对特定 IntelliTrace 事件的记录。  
  
 如果在进行调试，请停止调试。 Go to **Tools / Options / IntelliTrace / IntelliTrace Events**. 选择想要 IntelliTrace 记录的事件。  
  
## <a name="GoingFurther"></a> Collect IntelliTrace events and call information  
 默认情况下不启用此选项，但 IntelliTrace 可以随事件一起记录方法调用。 To enable collection of method calls go to **Tools / Options / IntelliTrace / General**, and select **IntelliTrace events and call information**.  
  
 这使你可以查看调用堆栈历史记录以及在代码中的调用间后退和前进。 IntelliTrace 记录的数据包括方法名、方法进入和退出点，以及部分参数值和返回值。  
  
> [!TIP]
> 默认情况下不启用此选项，因为它会增加大量开销。 IntelliTrace 不仅需要截获应用程序生成的每个方法调用，当需要在屏幕上显示数据或将数据保留到磁盘时，它还需要处理一组更大的数据。  
>   
> 可以通过限制 IntelliTrace 记录的事件列表以及将收集的模块数保持为最小值来减少性能开销。 有关详细信息，请参阅[控制 IntelliTrace 记录的调用信息量](../debugger/intellitrace-features.md#ControlCallData)。  
  
### <a name="using-the-navigation-gutter"></a>使用导航线  
 可以使用代码窗口左侧显示的导航线。 If you don't see the navigation gutter, go to **Tools / Options / IntelliTrace / Advanced**, and select **Display the navigation gutter while in debug mode**.  
  
 导航线让你能够在历史调试模式下向前和向后移动方法调用和事件。 有关历史调试的详细信息，请参阅[历史调试](../debugger/historical-debugging.md)。 它拥有多个命令：  
  
|||  
|-|-|  
|**在此设置调试器上下文**|将调试上下文设置为调用出现的调用时间范围。<br /><br /> 此图标仅在当前调用堆栈上显示。|  
|**返回调用站点**|将指针和调试上下文移回调用当前函数的位置。<br /><br /> 如果处于实时调试模式下，则此命令会启用历史调试。 如果向后定位到原始执行中断，则会禁用历史调试并启用实时调试。|  
|**转到上一个调用或 IntelliTrace 事件**|将指针和调试上下文移回上一个调用或事件。<br /><br /> 如果处于实时调试模式下，则此命令会启用历史调试。|  
|**单步执行**|单步执行当前选择的函数。<br /><br /> 只有处于历史调试模式下时才能使用此命令。|  
|**转到下一个调用或 IntelliTrace 事件**|将指针和调试上下文移到存在 IntelliTrace 数据的下一个调用或事件。<br /><br /> 只有处于历史调试模式下时才能使用此命令。|  
|**转到实时模式**|返回实时调试模式。|  
  
### <a name="search-for-a-line-or-method-in-intellitrace"></a>在 IntelliTrace 中搜索某行或某个方法  
 仅当已启用方法调用信息时才可以搜索方法。 可以搜索 IntelliTrace 历史记录以查找特定行或方法。 暂停调试程序执行时，在函数正文内右键单击以查看上下文菜单，然后单击“在 IntelliTrace 中搜索此行”或“在 IntelliTrace 中搜索此方法”。  
  
### <a name="ControlCallData"></a> 控制 IntelliTrace 记录的调用信息量  
 默认情况下，IntelliTrace 记录解决方案使用的所有模块的信息。 可以将 IntelliTrace 设置为仅记录你感兴趣的模块的调用信息。 In **Tools / Options / IntelliTrace / Modules**, You can specify the modules to include or the modules to exclude from IntelliTrace. IntelliTrace 将仅收集你指定的模块中生成的事件，以及你感兴趣的模块内发生的方法调用。  
  
 若要添加多个模块，请在字符串的开头或结尾使用通配符 *。 对于模块名称，请使用文件名，而不是程序集名称。 不接受文件路径。  
  
 尝试将模块数保持为最小值。 因为要收集的数据变少，所以可以获得更好的性能。 UI 中的噪音也会减少，因为要浏览的数据变少。  
  
## <a name="SaveSession"></a> Saving IntelliTrace data to file  
 You can save the data that IntelliTrace has collected going to **Debug / IntelliTrace / Save IntelliTrace Session** while you are debugging and the application is in a break state. 如果应用程序仍在运行或如果你已经停止调试，则菜单项会被禁用，且你将无法保存 IntelliTrace 收集的数据。  
  
 You can configure IntelliTrace to automatically save to a file by going to **Tools / Options / IntelliTrace / Advanced** and selecting **Store IntelliTrace recordings in this directory**. 还可以为生成的文件配置固定大小，这会让 IntelliTrace 在空间不足时覆盖旧数据。 自动保存文件并启用 Visual Studio 承载进程 (vshost.exe) 时，Visual Studio 会为每个 IntelliTrace 会话创建两个文件。  
  
> [!TIP]
> 要节省磁盘空间，请在不再需要时禁用自动保存文件。 不会删除任何现有文件。 可以随时从上下文菜单按需保存到文件。  
  
 将 IntelliTrace 数据保存到文件中时，每个 IntelliTrace 从中进行收集的进程都将获得一个 .itrace 文件。 You can then open the .itrace file in Visual Studio by going to **File / Open / File** and selecting the .itrace file from the Open File dialog. 有关详细信息，请参阅[使用保存的 IntelliTrace 数据](../debugger/using-saved-intellitrace-data.md)。  
  
## <a name="blogs"></a>博客  
 [Visual Studio Enterprise 2015 中的 IntelliTrace](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)  
  
 [Walkthrough of Live Debugging using IntelliTrace in Visual Studio 2015 (Text Editor)](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor/)  
  
 [Walkthrough of Live Debugging using IntelliTrace in Visual Studio 2015 (Social Club)](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club/)  
  
 [IntelliTrace in Visual Studio Enterprise 2015 now supports attach!](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach/)  
  
 [Collect data from a windows service using the IntelliTrace Standalone Collector](https://devblogs.microsoft.com/devops/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector/)  
  
 [Editing the IntelliTrace collection plan](https://devblogs.microsoft.com/devops/editing-the-intellitrace-collection-plan/)  
  
 [Custom TraceSource and debugging using IntelliTrace](https://devblogs.microsoft.com/devops/custom-tracesource-and-debugging-using-intellitrace/)  
  
 [IntelliTrace Standalone Collector and Application Pools running under Active Directory accounts](https://devblogs.microsoft.com/devops/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts/)  
  
## <a name="forums"></a>论坛  
 [Visual Studio 调试器](https://go.microsoft.com/fwlink/?LinkId=262263)  
  
## <a name="videos"></a>视频  
 [IntelliTrace Experience](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)  
  
 [Microsoft Visual Studio Ultimate 2015 中的 IntelliTrace 调试历史记录](https://channel9.msdn.com/events/Ignite/2015/BRK3716)
