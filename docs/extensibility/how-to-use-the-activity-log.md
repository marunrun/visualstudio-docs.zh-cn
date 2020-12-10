---
title: 如何：使用活动日志 |Microsoft Docs
description: Vspackage 可以将消息写入活动日志。 了解如何使用活动日志在零售环境中调试 Vspackage。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2796b8537c0f94c02c91fddc73f6d913ba1b0c4c
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993570"
---
# <a name="how-to-use-the-activity-log"></a>如何：使用活动日志
Vspackage 可以将消息写入活动日志。 此功能对于在零售环境中调试 Vspackage 特别有用。

> [!TIP]
> 始终打开活动日志。 Visual Studio 将保留最后100条目的滚动缓冲区以及包含常规配置信息的前10个条目。

## <a name="to-write-an-entry-to-the-activity-log"></a>将条目写入活动日志

1. 将此代码插入 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 方法或除 VSPackage 构造函数之外的任何其他方法中：

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     此代码将获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> 服务并将其强制转换为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> 接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> 使用当前的区域性上下文将信息性项写入活动日志。

2. 加载 VSPackage 时 (通常在调用命令或打开窗口) 时，将文本写入活动日志。

## <a name="to-examine-the-activity-log"></a>检查活动日志

1. 用 [/log](../ide/reference/log-devenv-exe.md) 命令行开关运行 Visual Studio，在会话期间将 ActivityLog.xml 写入磁盘。

2. 关闭 Visual Studio 后，在子文件夹中查找 Visual Studio 数据的活动日志：

   <em> *% AppData%</em>\Microsoft\VisualStudio \\ \<version>\ActivityLog.xml*。

3. 用任何文本编辑器打开活动日志。 下面是典型条目：

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>可靠编程

因为活动日志是一项服务，所以活动日志在 VSPackage 构造函数中不可用。

在写入活动日志之前，应立即获取该日志。 请勿缓存或保存活动日志以供将来使用。

## <a name="see-also"></a>另请参阅

- [/Log (devenv.exe)](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackages 故障排除](../extensibility/troubleshooting-vspackages.md)
- [VSPackages](../extensibility/internals/vspackages.md)
