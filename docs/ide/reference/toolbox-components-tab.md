---
title: 工具箱，“组件”选项卡
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.CHOOSEITEMS.FrameworkComponents
- VS.CHOOSEITEMS.COMComponents
- VS.CHOOSEITEMS.UniversalWindowsComponents
helpviewer_keywords:
- Toolbox, Components tab
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17f040b9bb64c2192bc6b376f5d0397ee5438071
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747755"
---
# <a name="toolbox-components-tab"></a>工具箱，“组件”选项卡

显示可以添加到适用于 Windows 窗体的 Visual Basic 和 C# 设计器的组件。 除 Visual Studio 附带的 .NET 组件（如 <xref:System.Messaging.MessageQueue> 和 <xref:System.Diagnostics.EventLog> 组件）外，还可向此选项卡添加自己的组件或第三方组件。

要显示此选项卡，请打开 Windows 窗体设计器。 选择“视图” > 工具箱”   。 在“工具箱”中，选择“组件”选项卡   。

## <a name="components"></a>组件数

**BackgroundWorker**

创建可在单独的专用线程上运行操作的 <xref:System.ComponentModel.BackgroundWorker> 组件实例。 有关详细信息，请参阅 [BackgroundWorker 组件](/dotnet/framework/winforms/controls/backgroundworker-component)。

**DirectoryEntry**

创建 <xref:System.DirectoryServices.DirectoryEntry> 组件实例，它封装 Active Directory 层次结构中的节点或对象，可用于与 Active Directory 服务提供商交互。

**DirectorySearcher**

创建 <xref:System.DirectoryServices.DirectorySearcher> 组件实例，该实例可用于对 Active Directory 执行查询。

**ErrorProvider**

创建 <xref:System.Windows.Forms.ErrorProvider> 组件实例，该实例向最终用户指示窗体上的控件具有与其关联的错误。 有关详细信息，请参阅 [ErrorProvider 组件](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)。

**EventLog**

创建 <xref:System.Diagnostics.EventLog> 组件实例，该实例可用于与系统和自定义事件日志进行交互，包括将事件写入日志和读取日志数据。

**FileSystemWatcher**

创建 <xref:System.IO.FileSystemWatcher> 组件实例，该实例可用于监视你有权访问的任何目录或文件的更改。

**HelpProvider**

创建为控件提供弹出帮助或联机帮助的 <xref:System.Windows.Forms.HelpProvider> 组件实例。 有关详细信息，请参阅 [HelpProvider 组件](/dotnet/framework/winforms/controls/helpprovider-component-windows-forms)。

**ImageList**

创建 <xref:System.Windows.Forms.ImageList> 组件实例，该实例提供管理 <xref:System.Drawing.Image> 对象集合的方法。 有关详细信息，请参阅 [ImageList 组件](/dotnet/framework/winforms/controls/imagelist-component-windows-forms)。

**MessageQueue**

创建 <xref:System.Messaging.MessageQueue> 组件实例，该实例可用于与消息队列进行交互，包括从队列读取消息和向队列写入消息、处理事务以及执行队列管理任务。

**PerformanceCounter**

创建 <xref:System.Diagnostics.PerformanceCounter> 组件实例，该实例可用于与 Windows 性能计数器进行交互，包括创建新类别和实例、从计数器读取值以及对计数器数据执行计算。

**Process**

创建 <xref:System.Diagnostics.Process> 组件实例，可用于停止、启动和操作与系统上的进程关联的数据。

**SerialPort**

创建 <xref:System.IO.Ports.SerialPort> 组件实例，该实例提供同步和事件驱动 I/O、提供对插针和中断状态的访问以及对串行驱动程序属性的访问。

**ServiceController**

创建 <xref:System.ServiceProcess.ServiceController> 组件实例，该实例可用于操作现有服务，包括启动和停止服务及向其发送命令。

**计时器**

创建 <xref:System.Windows.Forms.Timer> 组件实例，该实例可用于向基于 Windows 的应用程序添加基于时间的功能。 有关详细信息，请参阅 [Timer 组件](/dotnet/framework/winforms/controls/timer-component-windows-forms)。

> [!NOTE]
> 此外，还有一个基于系统的 <xref:System.Timers.Timer>，可将其添加到“工具箱”。此 <xref:System.Timers.Timer> 针对服务器应用程序进行了优化，Windows 窗体 <xref:System.Windows.Forms.Timer> 最适合在 Windows 窗体上使用  。

## <a name="see-also"></a>请参阅

- [在 Windows 窗体上使用的控件](/dotnet/framework/winforms/controls/controls-to-use-on-windows-forms)
- [“选择工具箱项”、“WPF 组件”](choose-toolbox-items-wpf-components.md)
- [工具箱](../../ide/reference/toolbox.md)