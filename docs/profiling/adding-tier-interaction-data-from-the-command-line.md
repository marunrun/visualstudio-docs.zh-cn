---
title: 从命令行添加层交互数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tier interaction profiling method
- profiling tools,tier interaction method
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 20b8438243382b28cccb510894d1674aa5872946
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779865"
---
# <a name="add-tier-interaction-data-from-the-command-line"></a>从命令行添加层交互数据

层交互分析提供有关多层应用程序函数中同步 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] 调用执行时间的附加信息，这些应用程序可与一个或多个数据库进行通信。

**Windows 8 和 Windows Server 2012**

若要收集有关 Windows 8 桌面应用 和 Windows Server 2012 应用的层交互数据，必须使用检测方法。 不支持收集有关 UWP 应用的层交互数据。

**Visual Studio 版本**

可以使用任何版本的 Visual Studio 收集层交互分析。 但是，层交互分析数据只能在 Visual Studio Enterprise 中查看。

**在远程计算机上收集 TIP 数据**

若要在远程计算机上收集层交互数据，必须从 Visual Studio 计算机的 %VSInstallDir%\Team Tools\Performance Tools\Setups 文件夹中将 vs_profiler **\_Platform>** _Language>.exe 文件复制到远程计算机上并进行安装\<_ **\_** _\<_    。 不能使用[远程调试](../debugger/remote-debugging.md)下载包中的分析工具。

**TIP 报告**

只能在 Visual Studio Enterprise 中查看层交互数据。 通过 [VSPerfReport](../profiling/vsperfreport.md) 生成的基于文件的层交互报告不可用。

## <a name="add-tier-interaction-data-with-vsperfcmd"></a>通过 VSPerfCmd 添加层交互数据

通过 VSPerfASPNETCmd 命令行工具可访问分析工具中可用的完整功能。 若要将层交互添加到使用 VSPerfCmd 收集的分析数据，必须使用 **VSPerfCLREnv** 实用工具设置并删除启用层交互数据的环境变量。 指定的选项和收集数据所需的过程取决于要分析的应用程序类型。

## <a name="profile-stand-alone-applications"></a>分析独立应用程序

若要将层交互数据添加到并非由另一进程运行的应用程序（例如 Windows 桌面应用程序，其对 SQLServer 数据库进行同步 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] 调用），请使用 **VSPerfClrEnv /InteractionOn** 选项设置环境变量，并使用 **VSPerfClrEnv /InteractionOff** 选项将其删除。

在下面的示例中，使用检测方法分析 Windows 桌面应用程序，并收集层交互数据。

### <a name="profile-a-windows-desktop-application-example"></a>分析 Windows 桌面应用程序示例

1. 使用管理员特权打开命令提示符窗口。 单击“开始”  ，指向“所有程序”  ，再指向“附件”  。 右键单击“命令提示符”  ，然后单击“以管理员身份运行”  。

2. 初始化 .NET 分析和 TIP 环境变量。 键入以下命令：

    ```cmd
    vsperfclrenv /traceon
    vsperfclrenv /interactionon
    ```

3. 启动探查器。 键入以下命令：

    ```cmd
    vsperfcmd /start:trace /output:Desktop_tip.vsp
    ```

4. 使用 VSPerfCmd 启动应用程序。 键入以下命令：

    ```cmd
    vsperfcmd /launch:DesktopApp.exe
    ```

5. 使用应用程序收集分析数据，然后以常规方式关闭应用程序。

6. 清除 TIP 环境变量。 键入以下命令：

    ```cmd
    vsperfclrenv /off
    ```

有关详细信息，请参阅[分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)。

## <a name="profile-services"></a>分析服务

若要分析包括 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序在内的服务，请使用 **VSPerfClrEnv /GlobalInteractionOn** 选项设置环境变量，并使用 **VSPerfClrEnv /GlobalInteractionOff** 选项将其删除。

分析包括 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序在内的服务时，通常需要重启计算机以启用分析。

在下面的示例中，使用检测方法分析 Windows 服务，并收集层交互数据。

### <a name="profile-a-windows-service-example"></a>分析 Windows 服务示例

1. 必要时请安装该服务。

2. 使用管理员特权打开命令提示符窗口。 单击“开始”  ，指向“所有程序”  ，再指向“附件”  。 右键单击“命令提示符”  ，然后单击“以管理员身份运行”  。

3. 初始化 .NET 分析环境变量。 键入以下命令：

    ```cmd
    vsperfclrenv /globaltraceon
    ```

4. 初始化 TIP 环境变量。 键入以下命令：

    ```cmd
    vsperfclrenv /globalinteractionon
    ```

5. 重启计算机，注册环境变量。

6. 使用管理员特权打开命令提示符窗口。

7. 启动探查器。 键入以下命令：

    ```cmd
    vsperfcmd /start:trace /output:MiddleTier_tip.vsp /user:SYSTEM /crosssession
    ```

8. 必要时，请启动该服务。

9. 将探查器附加到该服务。 键入以下命令：

    ```cmd
    vsperfcmd /attach:MiddleTier.exe /output:MyService_tip.vsp /user:SYSTEM /crosssession
    ```

10. 使用该服务并收集分析数据。

11. 停止使用探查器。 键入以下命令：

     `vsperfcmd /detach`

12. 清除 .NET 和 TIP 分析环境变量。 键入以下命令：

    ```cmd
    vsperfclrenv /globaloff
    ```

13. 重启计算机，注册清除的环境变量。

有关更多信息，请参见下列主题之一：

[分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)

[分析服务](../profiling/command-line-profiling-of-services.md)

## <a name="add-tier-interaction-data-with-vsperfaspnetcmd"></a>通过 VSPerfASPNETCmd 添加层交互数据

通过 VSPerfASPNETCmd 命令行工具可轻松分析 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序。 与 **VSPerfCmd** 命令行工具相比，它减少了选项、不必设置任何环境变量且无需重启计算机。 通过 VSPerfASPNETCmd 的这些功能可轻松收集层交互数据。

若要将层交互添加到使用 VSPerfASPNETCmd 收集的分析数据，请将 **/TIP** 选项添加到命令行。 例如，使用下面的命令行，通过检测方法收集 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web 应用程序的层交互数据：

```cmd
vsperfaspnetcmd /tip /trace http://localhost/MyWebApp
```

有关 VSPerfASPNETCmd 的详细信息，请参阅[使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)。
