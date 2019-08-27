---
title: 可视化工具体系结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 6aad395f-7170-4d9e-b2b8-a5faf453380e
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 82dd990a44984d2e3cc1c84244fbe07ea519fdfc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189036"
---
# <a name="visualizer-architecture"></a>可视化工具体系结构
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

调试器可视化工具的结构由两部分组成：  
  
- “调试器端”在 Visual Studio 调试器中运行  。 调试器端代码创建并显示可视化工具的用户界面。  
  
- “调试对象端”在 Visual Studio 正在调试的进程（“调试对象”）中运行   。  
  
  可视化工具是一个调试器组件，借助它，调试器即可以一种有意义且易理解的方式将数据对象的内容显示（“可视化”）出来  。 某些可视化工具还支持数据对象编辑。 通过编写自定义可视化工具，可以扩展调试器的功能，使其能够处理你自己的自定义数据类型。  
  
  要进行可视化处理的数据对象位于要调试的进程（“调试对象”进程）中  。 用于显示数据的用户界面在 Visual Studio 调试器进程内创建：  
  
|调试器进程|调试对象进程|  
|----------------------|----------------------|  
|调试器用户界面（数据提示、监视窗口、快速监视）|要可视化的数据对象|  
  
 若要在调试器界面中可视化数据对象，则需要一些代码，以实现两个进程间的通信。 由此可见，可视化工具的体系结构由两部分组成：“调试器端”代码和“调试对象端”代码   。  
  
 调试器端代码用于创建其自身用户界面，该界面可从调试器界面调用，例如数据提示、监视窗口或快速监视。 可以使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> 类和 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> 界面来创建可视化工具界面。 与所有的可视化工具 API 一样，DialogDebuggerVisualizer 和 IDialogVisualizerService 可在 <xref:Microsoft.VisualStudio.DebuggerVisualizers> 命名空间中找到。  
  
|调试器端|调试对象端|  
|-------------------|-------------------|  
|DialogDebuggerVisualizer 类<br /><br /> IDialogVisualizerService 界面|数据对象|  
  
 用户界面可从位于调试器端的对象提供程序获得要可视化的数据：  
  
|调试器端|调试对象端|  
|-------------------|-------------------|  
|DialogDebuggerVisualizer 类<br /><br /> IDialogVisualizerService 界面|数据对象|  
|对象提供程序（实现 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider>）||  
  
 调试对象端有一个对应的对象，称作对象源：  
  
|调试器端|调试对象端|  
|-------------------|-------------------|  
|DialogDebuggerVisualizer 类<br /><br /> IDialogVisualizerService 界面|数据对象|  
|对象提供程序（实现 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider>）|对象源（从 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> 派生）|  
  
 对象提供程序向可视化工具用户界面提供要可视化的对象数据。 这些数据对象是对象提供程序从对象源获得的。 对象提供程序和对象源提供 API，以便在调试器端和调试对象端之间传输对象数据。  
  
 每个可视化工具都必须获得要可视化的数据对象。 下表给出了对象提供程序和对象源用于此目的的相应 API：  
  
|对象提供程序|对象源|  
|---------------------|-------------------|  
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A><br /><br /> — 或 —<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A>|  
  
 注意，对象提供程序既可使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A>，也可使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A>。 其个任何一个 API 均会针对对象源调用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A>。 调用<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A?displayProperty=fullName>填充在 [System.IO.Stream] （<!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  -->)，它表示要可视化的对象的序列化的形式。  
  
 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A?displayProperty=fullName> 将数据重新反序列化为对象形式，使你可以在使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> 创建的 UI 中显示该对象。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> 填写作为原始数据 <!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  -->其中你必须自己反序列化。 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A?displayProperty=fullName> 通过调用<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName>若要获取的序列化 <!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  -->然后反序列化数据。 如果 .NET 无法序列化该对象，而需要自定义序列化时，请使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName>。 在这种情况下，你还必须重写 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.Serialize%2A?displayProperty=fullName> 方法。  
  
 如果要创建只读可视化工具，则与 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A> 或 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A> 的单向通信就可满足要求。 如果要创建支持数据对象编辑的可视化工具，还必须进行其他操作。 你还必须能够将数据对象从对象提供程序返回给对象源。 下表给出了对象提供程序和对象源用于此目的的 API：  
  
|对象提供程序|对象源|  
|---------------------|-------------------|  
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A><br /><br /> — 或 —<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.CreateReplacementObject%2A>|  
  
 再次提请注意，对象提供程序可使用的 API 有两个。 数据将始终从发送对象提供程序作为对象源 <!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  -->但<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A>需要序列化的对象 <!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  --> 您自己。  
  
 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceObject%2A> 采用你提供的对象的序列化到 <!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  -->然后调用<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A>发送 <!-- TODO: review code entity reference <xref:assetId:///System.IO.Stream?qualifyHint=False&amp;autoUpgrade=True>  --> <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.CreateReplacementObject%2A>的唯一值。  
  
 使用其中任意一个 Replace 方法将在调试对象中创建一个新数据对象，然后用该对象代替要可视化的对象。 如果你要更改原始对象的内容但不替换它，请使用下表中给出的一个 Transfer 方法。 这些 API 可同时进行双向数据传输，而无需替换要可视化的对象：  
  
|对象提供程序|对象源|  
|---------------------|-------------------|  
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.TransferData%2A><br /><br /> — 或 —<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.TransferObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.TransferData%2A>|  
  
## <a name="see-also"></a>请参阅  
 [如何：编写可视化工具](../debugger/how-to-write-a-visualizer.md)   
 [演练：用 C# 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)   
 [演练：用 Visual Basic 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)   
 [演练：用 Visual Basic 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)   
 [可视化工具安全注意事项](../debugger/visualizer-security-considerations.md)
