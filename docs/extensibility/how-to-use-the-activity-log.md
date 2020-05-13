---
title: 如何：使用活动日志 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 64986be303370cf8c9048612ff3d44e82e96805a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710584"
---
# <a name="how-to-use-the-activity-log"></a>如何：使用活动日志
VS包可以将消息写入活动日志。 此功能对于在零售环境中调试 VSPackages 特别有用。

> [!TIP]
> 活动日志始终处于打开状态。 Visual Studio 保留最近 100 个条目的前 10 个条目的滚动缓冲区以及前 10 个条目，这些条目具有常规配置信息。

## <a name="to-write-an-entry-to-the-activity-log"></a>将条目写入活动日志

1. 在<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法或任何其他方法中插入此代码，但 VSPackage 构造函数除外：

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     此代码获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>服务并将其转换为<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A>使用当前文化上下文将信息条目写入活动日志。

2. 加载 VSPackage 时（通常在调用命令或打开窗口时），文本将写入活动日志。

## <a name="to-examine-the-activity-log"></a>检查活动日志

1. 使用[/Log](../ide/reference/log-devenv-exe.md)命令行开关运行 Visual Studio，在会话期间将 ActivityLog.xml 写入磁盘。

2. 关闭 Visual Studio 后，在可视化工作室数据的子文件夹中查找活动日志：

   <em> *%AppData%</em>[微软]VisualStudio\\\<版本>_活动日志.xml*。

3. 使用任何文本编辑器打开活动日志。 下面是一个典型的条目：

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>可靠编程

由于活动日志是服务，因此在 VSPackage 构造函数中，活动日志不可用。

您应该在写入活动日志之前获取活动日志。 不要缓存或保存活动日志以供将来使用。

## <a name="see-also"></a>请参阅

- [/日志 （devenv.exe）](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackages 故障排除](../extensibility/troubleshooting-vspackages.md)
- [VSPackage](../extensibility/internals/vspackages.md)
