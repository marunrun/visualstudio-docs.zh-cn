---
title: 安装的命令行参数示例
description: 自定义这些示例，以创建自己的 Visual Studio 命令行安装。
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 837F31AA-F121-46e9-9996-F8BCE768E579
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 095fbcf35337ff2a619b6f3dcc6d5c28773ae975
ms.sourcegitcommit: 7b07e7b5e06e2e13f622445c568b78a284e1a40d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76542641"
---
# <a name="command-line-parameter-examples-for-visual-studio-installation"></a>Visual Studio 安装的命令行参数示例

为了说明如何[使用命令行参数来安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)，本文介绍了多个示例，你可以根据自己的需求自定义这些示例。

在每个示例中，`vs_enterprise.exe`、`vs_professional.exe` 和 `vs_community.exe` 表示 Visual Studio 安装引导程序的相应版本，这是启动下载过程的小型（大约 1 MB）文件。 若要使用其他版本，请用相应的安装引导程序名称进行替换。

> [!NOTE]
> 所有命令都需要进行管理提升，如果没有通过提升的提示符启动进程，将显示用户帐户控制提示。
>
> [!NOTE]
> 可以在命令行末尾使用 `^` 字符，将多行连接到一个命令中。 也可以直接在一行中编写这些代码行。 在 PowerShell 中，等效字符为反引号 (`` ` ``)。

有关可使用命令行安装的工作负载和组件列表，请参阅 [Visual Studio 工作负载和组件 ID](workload-and-component-ids.md) 页。

## <a name="using---installpath"></a>Using --installPath

* 安装 Visual Studio 的最小实例，不显示任何交互式提示，但显示进度：

  ```cmd
   vs_enterprise.exe --installPath C:\minVS ^
   --add Microsoft.VisualStudio.Workload.CoreEditor ^
   --passive --norestart
  ```

* 使用命令行更新 Visual Studio 实例（不显示任何交互式提示，但显示进度）：

   ```cmd
   vs_enterprise.exe --update --quiet --wait
   vs_enterprise.exe update --wait --passive --norestart --installPath "C:\installPathVS"
   ```

  > [!NOTE]
  > 这两个命令都是必需的。 第一个命令用于更新 Visual Studio 安装程序。 第二个命令用于更新 Visual Studio 实例。 为了避免看到“用户帐户控制”对话框，请以管理员身份运行命令提示符。

* 无提示安装包含法语语言包的 Visual Studio 桌面实例，仅在产品安装后才返回值。

  ```cmd
   vs_enterprise.exe --installPath C:\desktopVS ^
   --addProductLang fr-FR ^
   --add Microsoft.VisualStudio.Workload.ManagedDesktop ^
   --includeRecommended --quiet --wait
  ```

## <a name="using---wait"></a>使用 --wait

* 在批处理文件或脚本中使用，以等待 Visual Studio 安装程序完成之后再执行下一个命令。 对于批文件，`%ERRORLEVEL%` 环境变量包含命令的返回值，如[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页面所述。 某些命令实用程序需要其他参数，以等待完成并获取安装程序的返回值。 以下是与 PowerShell 脚本命令“Start-Proces”搭配使用的其他参数的示例：

   ```cmd
   start /wait vs_professional.exe --installPath "C:\VS" --passive --wait > nul
   echo %errorlevel%
   ```

   ```powershell
   $exitCode = Start-Process -FilePath vs_enterprise.exe -ArgumentList "--installPath", "C:\VS", "--passive", "--wait" -Wait -PassThru
   ```

   or

   ```powershell
    $startInfo = New-Object System.Diagnostics.ProcessStartInfo
    $startInfo.FileName = "vs_enterprise.exe"
    $startInfo.Arguments = "--all --quiet --wait"
    $process = New-Object System.Diagnostics.Process
    $process.StartInfo = $startInfo
    $process.Start()
    $process.WaitForExit()
   ```

* 第一个“--wait”由 Visual Studio 安装程序使用，第二个“--Wait”由“Start-Process”用于等待完成。 “-PassThru”参数由“Start-Process”使用，以以将安装程序的退出代码用于其返回值。

## <a name="using---layout"></a>Using --layout

* 下载 Visual Studio 核心编辑器（最起码的 Visual Studio 配置）。 仅包括英语语言包：

  ```cmd
   vs_community.exe --layout C:\VS ^
   --lang en-US ^
   --add Microsoft.VisualStudio.Workload.CoreEditor
  ```

* 下载 .NET 桌面和 .NET Web 工作负载，以及所有推荐组件和 GitHub 扩展。 仅包括英语语言包：

  ```cmd
   vs_community.exe --layout C:\VS ^
   --lang en-US ^
   --add Microsoft.VisualStudio.Workload.NetWeb ^
   --add Microsoft.VisualStudio.Workload.ManagedDesktop ^
   --add Component.GitHub.VisualStudio ^
   --includeRecommended
  ```

## <a name="using---all"></a>使用 --all

* 启动交互式安装 Visual Studio Enterprise 版本中的所有工作负载和组件：

   ```cmd
   vs_enterprise.exe --all
   ```

## <a name="using---includerecommended"></a>Using --includeRecommended

* 借助 Node.js 开发支持，在已安装 Visual Studio Community 版本的计算机上安装 Visual Studio Professional 的第二个命名实例：

   ```cmd
   vs_professional.exe --installPath C:\VSforNode ^
   --add Microsoft.VisualStudio.Workload.Node --includeRecommended --nickname VSforNode
  ```

## <a name="using---remove"></a>Using --remove

::: moniker range="vs-2017"

* 从默认安装的 Visual Studio 实例中删除分析工具组件：

  ```cmd
   vs_enterprise.exe modify ^
   --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" ^
   --remove Microsoft.VisualStudio.Component.DiagnosticTools ^
   --passive
  ```

::: moniker-end

::: moniker range="vs-2019"

* 从默认安装的 Visual Studio 实例中删除分析工具组件：

  ```cmd
   vs_enterprise.exe modify ^
   --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" ^
   --remove Microsoft.VisualStudio.Component.DiagnosticTools ^
   --passive
  ```

::: moniker-end

## <a name="using---path"></a>Using --path

::: moniker range="vs-2017"

这些命令行参数是 15.7 版中的新内容  。 有关这些参数的详细信息，请参阅[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页。

::: moniker-end

* 使用安装、缓存和共享路径：

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path cache="C:\VS\cache" --path shared="C:\VS\shared"`

* 仅使用安装和缓存路径：

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path cache="C:\VS\cache"`

* 仅使用安装和共享路径：

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS" --path shared="C:\VS\shared"`

* 仅使用安装路径：

  `vs_enterprise.exe --add Microsoft.VisualStudio.Workload.CoreEditor --path install="C:\VS"`

## <a name="using-export"></a>使用 export

::: moniker range="vs-2017"

此命令行命令是 15.9 版中的新内容  。 有关此命令行命令的详细信息，请参阅[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页。

::: moniker-end

* 使用 export 保存安装中的选择：

  ```cmd
  "C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe" export --installPath "C:\VS" --config "C:\.vsconfig"
  ```

* 使用 export 从头开始保存自定义选择：

  ```cmd
  "C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe" export --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --config "C:\.vsconfig"
  ```

## <a name="using---config"></a>使用 --config

::: moniker range="vs-2017"

此命令行参数是 15.9 版中的新内容  。 有关此命令行命令的详细信息，请参阅[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页。

::: moniker-end

* 使用 --config 从以前保存的安装配置文件安装工作负载和组件：

  ```cmd
  vs_enterprise.exe --config "C:\.vsconfig" --installPath "C:\VS"
  ```

* 使用 --config 向现有安装添加工作负载和组件：

  ```cmd
  vs_enterprise.exe modify --installPath "C:\VS" --config "C:\.vsconfig"
  ```

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)
* [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
