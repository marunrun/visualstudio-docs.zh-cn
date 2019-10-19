---
title: 工具箱，“组件”选项卡 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Toolbox, Components tab
ms.assetid: 332fafab-a763-4244-b388-15d1b5b5cc04
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ce18767d95b3ac539737d78acbd2259dcda0a036
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661572"
---
# <a name="toolbox-components-tab"></a>工具箱，“组件”选项卡
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

显示可以添加到 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 和 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 设计器的组件。 除 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 附带的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 组件（如 <xref:System.Messaging.MessageQueue> 和 <xref:System.Diagnostics.EventLog> 组件）外，还可向此选项卡添加自己的组件或第三方组件。有关详细信息，请参阅[如何：操作工具箱选项卡](https://msdn.microsoft.com/21285050-cadd-455a-b1f5-a2289a89c4db)。

 若要显示此选项卡，请从“视图”  菜单中选择“工具箱”  。 在“工具箱”  中，选择“组件”  选项卡。

 **BackgroundWorker**创建一个 `System.ComponentModel.BackgroundWorker` 组件实例，该实例可在单独的专用线程上运行操作。

 **DirectoryEntry**创建一个 <xref:System.DirectoryServices.DirectoryEntry> 组件实例，该实例封装 Active Directory 层次结构中的节点或对象，并可用于与 Active Directory 服务提供程序进行交互。

 **DirectorySearcher**创建一个 <xref:System.DirectoryServices.DirectorySearcher> 组件实例，该实例可用于对 Active Directory 执行查询。

 **ErrorProvider**创建一个 `System.Windows.Forms.ErrorProvider` 组件实例，该实例向最终用户指示窗体上的某个控件具有与其相关联的错误。

 **EventLog**创建可用于与系统和自定义事件日志进行交互的 <xref:System.Diagnostics.EventLog> 组件实例，包括将事件写入日志和读取日志数据。 有关详细信息，请参阅 [EventLog 组件简介](https://msdn.microsoft.com/a2ba4f28-4b1a-435e-99ef-51b28e21f805)。

 **FileSystemWatcher**创建一个 <xref:System.IO.FileSystemWatcher> 组件实例，该实例可用于监视对您有权访问的任何目录或文件所做的更改。 有关详细信息，请参阅[如何：配置 FileSystemWatcher 组件实例](https://msdn.microsoft.com/2e628234-4951-4135-8a86-28b924070d50)。

 **HelpProvider**创建一个 `System.Windows.Forms.HelpProvider` 组件实例，该实例为控件提供弹出帮助或联机帮助。

 **ImageList**创建一个 `System.Windows.Forms.ImageList` 组件实例，该实例提供管理 `System.Drawing.Image` 对象集合的方法。

 **MessageQueue**创建一个 <xref:System.Messaging.MessageQueue> 组件实例，该实例可用于与消息队列进行交互，包括从队列读取消息和向队列写入消息、处理事务以及执行队列管理任务。 有关详细信息，请参阅[使用消息传送组件](https://msdn.microsoft.com/922dbac7-26f0-4e39-b666-ccfc184793d7)。

 **PerformanceCounter**创建一个 <xref:System.Diagnostics.PerformanceCounter> 组件实例，该实例可用于与 Windows 性能计数器进行交互，包括创建新类别和实例、从计数器读取值以及对计数器数据执行计算。 有关详细信息，请参阅[监视性能阈值](https://msdn.microsoft.com/b8b44a55-31d0-4b45-9517-8c1b1e4fdc91)。

 **处理**创建一个 <xref:System.Diagnostics.Process> 组件实例，该实例可用于停止、启动和操作与系统上的进程关联的数据。 有关详细信息，请参阅[监视和管理 Windows 进程](https://msdn.microsoft.com/a86bd4c1-b92c-49a0-8f32-61d67837b45e)。

 **SerialPort**创建一个 `System.IO.Ports.SerialPort` 组件实例，该实例提供同步和事件驱动 i/o、对插针和中断状态的访问以及对串行驱动程序属性的访问。

 **ServiceController**创建一个 <xref:System.ServiceProcess.ServiceController> 组件实例，该实例可用于操作现有服务，包括启动和停止服务并向其发送命令。 有关详细信息，请参阅[监视 Windows 服务](https://msdn.microsoft.com/4542ee3f-e052-4cb9-8726-58e9420de222)。

 **计时器**创建可用于向基于 Windows 的应用程序添加基于时间的功能的 <xref:System.Windows.Forms.Timer> 组件实例。 有关详细信息，请参阅 [Timer 组件](https://msdn.microsoft.com/library/6700e534-6382-43d5-98ed-14205435fff7)。

> [!NOTE]
> 此外，还有一个基于系统的 <xref:System.Timers.Timer>，可将其添加到“工具箱”。此 <xref:System.Timers.Timer> 针对服务器应用程序进行了优化，Windows 窗体 <xref:System.Windows.Forms.Timer> 最适合在 Windows 窗体上使用  。

## <a name="see-also"></a>另请参阅
 [通过组件编程](https://msdn.microsoft.com/library/d4d4fcb4-e0b8-46b3-b679-7ee0026eb9e3)[演练](https://msdn.microsoft.com/library/373cacf7-479e-4b05-991c-5cb18824e913) ["工具箱" "](../../ide/reference/toolbox.md) [选择工具箱项" 对话框（Visual Studio）](https://msdn.microsoft.com/bd07835f-18a8-433e-bccc-7141f65263bb)
