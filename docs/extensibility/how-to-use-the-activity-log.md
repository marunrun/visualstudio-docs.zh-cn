---
title: 如何：使用活动日志 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 53888f85a41fdd5bef3985c4da986609a032e377
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309354"
---
# <a name="how-to-use-the-activity-log"></a>如何：使用活动日志
Vspackage 可以将消息写入活动日志。 此功能是非常适合在零售环境中进行调试的 Vspackage。

> [!TIP]
> 活动日志始终开启。 Visual Studio 将最近 100 个项，以及具有常规配置信息的前 10 个项一个循环缓冲区。

## <a name="to-write-an-entry-to-the-activity-log"></a>若要向活动日志写入条目

1. 此代码中的插入<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法或任何其他方法，但 VSPackage 构造函数中：

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     此代码获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>服务并将强制转换到<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> 写入到活动日志中，使用当前区域性上下文的信息项。

2. 加载 VSPackage 时 （通常在调用命令或打开一个窗口时），会在活动日志中写入文本。

## <a name="to-examine-the-activity-log"></a>活动日志中检查

1. 运行 Visual Studio 中使用[/log](../ide/reference/log-devenv-exe.md)命令行开关在会话期间将 ActivityLog.xml 写入到磁盘。

2. 关闭 Visual Studio 后, 找到活动日志的子文件夹中的 Visual Studio 数据：

   <em> *%AppData%</em>\Microsoft\VisualStudio\\\<version>\ActivityLog.xml*.

3. 使用任何文本编辑器打开活动日志。 以下是典型条目：

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>可靠编程

活动日志是一项服务，因为活动日志是在 VSPackage 构造函数中不可用。

应写入之前先获取活动日志。 不要缓存或保存活动日志以供将来使用。

## <a name="see-also"></a>请参阅

- [/Log (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackages 故障排除](../extensibility/troubleshooting-vspackages.md)
- [VSPackage](../extensibility/internals/vspackages.md)
