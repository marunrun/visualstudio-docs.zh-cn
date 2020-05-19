---
title: 创建自定义数据可视化工具 | Microsoft Docs
ms.date: 11/07/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.visualizer.troubleshoot
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers
ms.assetid: c24c006f-f2ac-429f-89db-677fc0c6e1ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 64f44379c98808cb93fbe51498234a34a695c3d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62564714"
---
# <a name="create-custom-data-visualizers"></a>创建自定义数据可视化工具
 “可视化工具”是 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 调试器用户界面的一部分，该用户界面以适合其数据类型的方式显示变量或对象。 例如，HTML 可视化工具解释 HTML 字符串，并以与浏览器窗口中相同的方式显示结果。 位图可视化工具解释位图结构并显示它表示的图形。 某些可视化工具允许你修改数据，还允许你查看数据。

 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 调试器包括六个标准可视化工具。 文本、HTML、XML 和 JSON 可视化工具处理字符串对象。 WPF 树可视化工具显示 WPF 对象可视化树的属性。 数据集可视化工具适用于 DataSet、DataView 和 DataTable 对象。

可从 Microsoft、第三方和社区下载更多可视化工具。 还可以编写自己的可视化工具，并将它们安装在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 调试器中。

在调试器中，可视化工具由放大镜图标 ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")表示。 可以在 DataTip、调试器“监视”窗口中或“快速监视”对话框中选择图标，然后为相应对象选择适当的可视化工具  。

## <a name="write-custom-visualizers"></a>编写自定义可视化工具

 > [!NOTE]
 > 若要为本机代码创建自定义可视化工具，请参阅 [SQLite 本机调试器可视化器](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/SqliteVisualizer)示例。 UWP 和 Windows 8.x 应用不支持自定义可视化工具。

可以为任何托管类（除 <xref:System.Object> 和 <xref:System.Array> 之外）的对象编写自定义可视化工具。

调试器可视化工具的结构由两部分组成：

- “调试器端”在 Visual Studio 调试器中运行，并创建并显示可视化器用户界面。

- “调试对象端”在 Visual Studio 正在调试的进程（“调试对象”）中运行 。 要可视化的数据对象（如 String 对象）存在在调试对象进程中。 调试对象端将对象发送到调试器端，调试器端会在你创建的用户界面中显示该对象。

调试器端从一个“对象提供程序”接收数据对象，该提供程序可实现 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> 接口。 调试对象端通过“对象源”发送对象，该对象源派生自 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>。

对象提供程序还可以将数据发送回对象源，这样你便能够编写可编辑数据的可视化工具。 可以重写此对象提供程序，以便与表达式计算器和对象源进行对话。

调试对象端和调试器端通过 <xref:System.IO.Stream> 方法相互通信，这些方法将数据对象序列化到 <xref:System.IO.Stream> 中，并将 <xref:System.IO.Stream> 反序列化回数据对象。

只有在一个泛型类型是开放类型时，才可以为其编写可视化工具。 此限制与使用 `DebuggerTypeProxy` 特性时的限制相同。 有关详细信息，请参阅[使用 DebuggerTypeProxy 属性](../debugger/using-debuggertypeproxy-attribute.md)。

自定义可视化工具可能有安全性问题。 请参阅[可视化工具安全注意事项](../debugger/visualizer-security-considerations.md)。

以下步骤提供了创建可视化工具的概括性介绍。 有关详细说明，请参阅[演练：用 C# 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)或[演练：用 Visual Basic 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)。

### <a name="to-create-the-debugger-side"></a>创建调试器端

若要在调试器端创建可视化工具用户界面，可以创建从 <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> 继承的类，并且重写 <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> 方法来显示界面。 可以使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> 在可视化工具中显示 Windows 窗体、对话框和控件。

1. 使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> 方法在调试器端获取可视化的对象。

1. 创建一个从 <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> 继承的类。

1. 重写 <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> 方法以显示接口。 使用 <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> 方法在界面中显示 Windows 窗体、对话框或控件。

4. 应用 <xref:System.Diagnostics.DebuggerVisualizerAttribute>，让可视化工具显示它 (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>)。

### <a name="to-create-the-debuggee-side"></a>创建调试对象端

使用 <xref:System.Diagnostics.DebuggerVisualizerAttribute> 指定调试对象端代码。

1. 应用 <xref:System.Diagnostics.DebuggerVisualizerAttribute>，为它指定可视化工具 (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>) 和对象源 (<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>)。 如果省略对象源，可视化工具将使用默认对象源。

1. 若要让可视化工具编辑并显示数据对象，请重写 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> 中的 `TransferData` 或 `CreateReplacementObject` 方法。

## <a name="see-also"></a>请参阅

- [演练：用 C# 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [演练：用 Visual Basic 编写可视化工具](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)
- [如何：测试和调试可视化工具](../debugger/how-to-test-and-debug-a-visualizer.md)
- [可视化工具 API 参考](../debugger/visualizer-api-reference.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)