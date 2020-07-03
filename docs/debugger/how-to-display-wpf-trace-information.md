---
title: 如何 - 显示 WPF 跟踪信息 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- WPF, debugging
- debugging, WPF
ms.assetid: be3c6859-06e1-459e-9fd0-46375b5f55ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 362376176cfb95c4e285f6837c53d277110e3439
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349778"
---
# <a name="how-to-display-wpf-trace-information"></a>如何：显示 WPF 跟踪信息
[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 可接收来自 WPF 应用程序的调试跟踪信息，并将该信息显示在“输出”窗口中。 若要显示调试跟踪信息，必须启用 WPF 跟踪。

 可以在 App.Config 文件中启用 WPF 跟踪，或通过使用 <xref:System.Diagnostics.PresentationTraceSources> 类以编程方式启用 WPF 跟踪。 启用 WPF 跟踪的一种更简单方式是使用“选项”窗口。 不支持针对 Web 应用程序的 WPF 跟踪。

### <a name="to-enable-or-customize-wpf-trace-information"></a>启用或自定义 WPF 跟踪信息

1. 在“工具”菜单上选择“选项” 。

2. 在“选项”对话框内左侧的框中，打开“调试”节点 。

3. 在“调试”下，单击“输出窗口” 。

4. 在“常规输出设置”下，选择“所有调试输出” 。

5. 在右侧的框中，查找“WPF 跟踪设置”。

6. 打开“WPF 跟踪设置”节点。

7. 在“WPF 跟踪设置”下，单击要启用的设置的类别（例如，“数据绑定”） 。

     “数据绑定”或单击的任何类别旁边的“设置”列中将出现一个下拉列表控件。

8. 单击该下拉列表，并选择希望看到的跟踪信息的类型：“全部”、“严重”、“错误”、“警告”、“信息”、“详细”或“ActivityTracing”      。

     如果选择“严重”，则仅启用“严重”事件的跟踪。

     如果选择“错误”，则启用“严重”和“错误”事件的跟踪。

     如果选择“警告”，则启用“严重”、“错误”和“警告”事件的跟踪。

     如果选择“信息”，则启用“严重”、“错误”、“警告”和“信息”事件的跟踪。

     如果选择“详细”，则启用“严重”、“错误”、“警告”、“信息”和“详细”事件的跟踪。

     如果选择“活动跟踪”，则启用“停止”、“启动”、“挂起”、“传输”和“继续”事件的跟踪。

     有关这些跟踪信息级别的含义的更多信息，请参见 <xref:System.Diagnostics.SourceLevels>。

9. 单击 **“确定”** 。

### <a name="to-disable-wpf-trace-information"></a>禁用 WPF 跟踪信息

1. 在“工具”菜单上选择“选项” 。

2. 在“选项”对话框内左侧的框中，打开“调试”节点 。

3. 在“调试”下，单击“输出窗口” 。

4. 在右侧的框中，查找“WPF 跟踪设置”。

5. 打开“WPF 跟踪设置”节点。

6. 在“WPF 跟踪设置”下，单击要启用的设置的类别（例如，“数据绑定”） 。

     “数据绑定”或单击的任何类别旁边的“设置”列中将出现一个下拉列表控件。

7. 单击该下拉列表并选择“关闭”。

8. 单击 **“确定”** 。

## <a name="see-also"></a>请参阅
- [调试 WPF](../debugger/debugging-wpf.md)