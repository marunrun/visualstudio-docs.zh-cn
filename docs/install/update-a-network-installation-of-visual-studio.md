---
title: 更新基于网络的安装
description: 了解如何使用 --layout 命令更新基于网络的 Visual Studio 安装
ms.date: 01/08/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 1AF69C0E-0AC9-451B-845D-AE4EDBCEA65C
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 774e189306345187ac6a0c29b7060cb5537e8adb
ms.sourcegitcommit: 10d16e18c5f5e482c4c2856e6cacaad283463b65
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776170"
---
# <a name="update-a-network-based-installation-of-visual-studio"></a>更新基于网络的 Visual Studio 安装

可以使用最新的产品更新来更新 Visual Studio 的网络安装布局，以便将它用作 Visual Studio 最新更新的安装点，同时还可用于维护已部署到客户端工作站的安装。

## <a name="how-to-update-a-network-layout"></a>如何更新网络布局

> [!IMPORTANT]
> 这些说明假定你之前已创建了一个网络安装布局。 要详细了解如何执行此操作，请参阅[创建 Visual Studio 的网络安装](create-a-network-installation-of-visual-studio.md)页面。

要刷新网络安装共享，使其包含最新更新，请运行 `--layout` 命令，从而以增量方式下载更新后的包。

::: moniker range="vs-2017"

**15.3 中的新增功能**：如果你在[首次创建网络布局](create-a-network-installation-of-visual-studio.md)时选择了部分布局，这些设置将被保存。 此后一切布局命令都将使用先前的选项以及任何指定的新选项。 但是，如果正在使用早期版本的布局，则应使用与首次创建网络安装布局相同的命令行参数（即相同的工作负载和语言）来更新其内容。

::: moniker-end

::: moniker range="vs-2019"

如果你在[首次创建网络布局](create-a-network-installation-of-visual-studio.md)时选择了部分布局，这些设置将被保存。 此后一切布局命令都将使用先前的选项以及任何指定的新选项。

::: moniker-end

如果在文件共享上托管布局，则应更新布局的私有副本（例如 c:\VSLayout），然后下载所有已更新内容，并将其复制到文件共享（例如 \\server\products\VS）。 如果不这样做，那么任何在布局更新时运行安装程序的用户，将更有可能无法通过布局获取所有内容，因为布局并未完全更新。

请浏览下面几个示例，它们说明如何创建并更新布局：

* 首先，以下示例说明如何通过一个工作负载来创建布局（仅限英语）：

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
  ```

* 将相同布局更新到较新版本的说明如下。 无需指定任何额外的命令行参数。 此布局文件夹中的任何后续布局命令都将使用先前所保存的设置。

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout
  ```

* 下面介绍如何以无人参与方式将布局更新为较新版本。 布局操作在新控制台窗口中运行设置进程。 该窗口保持打开状态，以便用户可以看到最终结果以及任何可能发生的错误的摘要。 如果以无人参与方式执行布局操作（例如，具有定期运行以将布局更新为最新版本的脚本），则使用 `--passive` 参数，进程会自动关闭窗口。

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --passive
  ```

* 添加额外工作负载和本地化语言的方法如下所示。  （此命令添加 Azure 开发工作负载。  ）现在，此布局中同时加入了托管桌面和 Azure。  这些工作负载中还同时加入了英语和德语的语言资源。  并且已将布局更新至最新的可用版本。

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
  ```

    > [!IMPORTANT]
    > 更新操作不会安装新添加的可选组件（即使将这些组件包含在[响应文件](automated-installation-with-response-file.md)的“添加”部分中）。 这是因为在更新期间未使用添加操作。
    >
    > **解决方法**：升级后运行单独的修改操作以安装缺少的组件。

* 最后，有关如何在不更新版本的前提下添加其他工作负载和本地化语言的说明详见此处。 （此命令添加“ASP.NET 和 Web 开发”工作负载  。）当前，托管桌面、Azure 以及 ASP.NET 和 Web 开发工作负载已加入此布局。 这些工作负载中还加入了英语、德语和法语的语言资源。  但在运行此命令时，布局不会更新至最新的可用版本。 它将维持现有版本。

  ```cmd
  vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.NetWeb --lang fr-FR --keepLayoutVersion
  ```

## <a name="deploy-an-update-to-client-machines"></a>将更新部署到客户端计算机

更新可以由企业管理员进行部署，也可以由客户端计算机启动，具体视网络环境的配置方式而定。

* 用户可以更新通过脱机安装文件夹安装的 Visual Studio 实例：
  * 运行 Visual Studio 安装程序。
  * 然后，单击“更新”  。

::: moniker range="vs-2017"

* 管理员可以单独使用下面两个命令，更新 Visual Studio 的客户端部署，而无需与任何用户进行交互：
  * 首先，更新 Visual Studio 安装程序： <br>```vs_enterprise.exe --quiet --update```
  * 然后，更新 Visual Studio 应用程序本身： <br>```vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" --quiet --wait --norestart```

::: moniker-end

::: moniker range="vs-2019"

* 管理员可以单独使用下面两个命令，更新 Visual Studio 的客户端部署，而无需与任何用户进行交互：
  * 首先，更新 Visual Studio 安装程序： <br>```vs_enterprise.exe --quiet --update```
  * 然后，更新 Visual Studio 应用程序本身： <br>```vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" --quiet --wait --norestart```

::: moniker-end

> [!NOTE]
> 使用 [vswhere.exe 命令](tools-for-managing-visual-studio-instances.md)可标识客户端计算机上 Visual Studio 现有实例的安装路径。
>
> [!TIP]
> 若要详细了解如何控制何时向用户显示更新通知，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)。

## <a name="verify-a-layout"></a>验证布局

使用 `--verify` 在提供的脱机缓存中执行验证。 它将检查包文件是否缺少或无效。 验证完成后，它将打印缺少的文件和无效文件的列表。

```cmd
vs_enterprise.exe --layout <layoutDir> --verify
```

可在 layoutDir 内调用 vs_enterprise.exe。

> [!NOTE]
> `--verify` 选项所需的某些重要元数据文件必须位于布局脱机缓存内部。 如果缺少这些元数据文件，则无法运行“--verify”，且安装程序会出错。 如果遇到此错误，请重新创建新脱机布局到其他文件夹（或到相同的脱机缓存文件夹）。 要执行此操作，请运行与创建初始脱机布局相同的布局命令。 例如 `vs_enterprise.exe --layout <layoutDir>`。

由于 Microsoft 定期为 Visual Studio 提供更新，因此新创建的布局与初始布局的版本可能不同。

> [!NOTE]
> 验证仅适用于 Visual Studio 的特定次要版本的最新版本。 发布新版本后，验证将不适用于同一次要版本的早期修补级别版本。

## <a name="fix-a-layout"></a>修复布局

使用 `--fix` 执行与 `--verify` 相同的验证，并尝试修复标识的问题。 `--fix` 过程需要 Internet 连接，因此在调用 `--fix` 前请确保计算机已连接至 Internet。

```cmd
vs_enterprise.exe --layout <layoutDir> --fix
```

可在 layoutDir 内调用 vs_enterprise.exe。

## <a name="remove-older-versions-from-a-layout"></a>从布局中删除旧版本

对脱机缓存执行布局更新后，布局缓存文件夹中可能存在某些已过时的包，最新版本的 Visual Studio 安装不再需要这些包。 可使用 `--clean` 选项从脱机缓存文件夹中删除已过时的包。

要执行此操作，需要前往目录清单的文件路径，其中包含这些已过时的包。 可在脱机布局缓存的“存档”文件夹中找到该目录清单。 更新布局时，这些目录清单就保存在此处。 在“存档”文件夹中，有一个或多个名为“GUID”的文件夹，其中每个都包含已过时的目录清单。 “GUID”文件夹数目应与脱机缓存的更新次数保持一致。

每个“GUID”文件夹中都保存着若干文件。 最重要的两个文件分别是“catalog.json”文件和“version.txt”文件。 “catalog.json”文件需要传递给 `--clean` 选项的已过时目录清单。 另一个 version.txt 文件则包含此已过时目录清单的版本。 根据版本号，可自行决定是否要从此目录清单中删除已过时包。 其他“GUID”文件夹中可执行同样的操作。 选择要清除的目录后，通过向这些目录提供文件路径来运行 `--clean` 命令。

以下几个示例说明了如何使用 --clean 选项：

```cmd
vs_enterprise.exe --layout <layoutDir> --clean <file-path-of-catalog1> <file-path-of-catalog2> …
```

```cmd
vs_enterprise.exe --layout <layoutDir> --clean <file-path-of-catalog1> --clean <file-path-of-catalog2> …
```

还可在 &lt;layoutDir&gt; 中调用 vs_enterprise.exe。 以下是一个示例：

```cmd
c:\VSLayout\vs_enterprise.exe --layout c:\VSLayout --clean c:\VSLayout\Archive\1cd70189-fc55-4583-8ad8-a2711e928325\Catalog.json --clean c:\VS2017Layout\Archive\d420889f-6aad-4ba4-99e4-ed7833795a10\Catalog.json
```

执行此命令时，安装程序会分析脱机缓存文件夹，以查找要删除的文件列表。 然后，可以对要删除的文件进行评审，并确认是否删除。

## <a name="get-support-for-your-offline-installer"></a>获取对脱机安装程序的支持

如果脱机安装遇到问题，请告知我们。 告知我们的最好方式是使用[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具。 使用此工具时，可发送我们诊断和修复问题所需的遥测数据和日志。

对于安装相关问题，我们还提供[实时聊天  ](https://visualstudio.microsoft.com/vs/support/#talktous)（仅限英语）支持选项。

我们还提供其他支持选项。 若要查看列表，请参阅[反馈](../ide/feedback-options.md)页面。

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
