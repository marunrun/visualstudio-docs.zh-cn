---
title: 创建基于网络的安装
description: 了解如何创建用于在企业中部署 Visual Studio 的网络安装点。
ms.date: 10/29/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e7bc45db427a517a9208833cc5be6977bfc62d03
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591471"
---
# <a name="create-a-network-installation-of-visual-studio"></a>创建 Visual Studio 的网络安装

通常情况下，企业管理员会创建网络安装点，以便部署到客户端工作站。 我们精心设计了 Visual Studio，可将初始安装的相关文件以及所有产品更新缓存到一个文件夹中。 （此过程也称为_创建布局_。）

这样即使尚未更新到最新的服务更新，客户端工作站也可以使用同一网络位置来管理其安装。

 > [!NOTE]
 > 如果企业使用多个 Visual Studio 版本（例如，同时使用 Visual Studio Professional 和 Visual Studio Enterprise），需要为每个版本单独创建网络安装共享。

## <a name="download-the-visual-studio-bootstrapper"></a>下载 Visual Studio 引导程序

下载适用于所需版本的 Visual Studio 的引导程序文件。 请确保选择“保存”，然后选择“打开文件夹”   。

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 的引导程序，请参阅 [Visual Studio 早期版本](https://visualstudio.microsoft.com/vs/older-downloads/)下载页，获取关于如何执行此操作的详细信息。

安装程序可执行文件&mdash;具体而言是引导程序文件&mdash;应与下面其中一项匹配，或与之类似。

| 版本 | Filename |
|-------------|-----------------------|
|Visual Studio Enterprise | **vs_enterprise.exe** |
|Visual Studio Professional | **vs_professional.exe** |
|Visual Studio 生成工具   | **vs_buildtools.exe** |

其他受支持的引导程序包括 **vs_feedbackclient.exe**、**vs_teamexplorer.exe**、**vs_testagent.exe**、**vs_testcontroller.exe** 和 **vs_testprofessional.exe**。

::: moniker-end

::: moniker range="vs-2019"

安装程序可执行文件&mdash;具体而言是引导程序文件&mdash;应与下面其中一项匹配，或与之类似。

|版本 | 下载|
|-------------|-----------------------|
|Visual Studio Enterprise | [**vs_enterprise.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
|Visual Studio Professional | [**vs_professional.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
| Visual Studio 生成工具   | [**vs_buildtools.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019) |

其他受支持的引导程序包括 [vs_teamexplorer.exe](https://aka.ms/vs/16/release/vs_teamexplorer.exe)、[vs_testagent.exe](https://aka.ms/vs/16/release/vs_testagent.exe) 和 [vs_testcontroller.exe](https://aka.ms/vs/16/release/vs_testcontroller.exe)。

::: moniker-end

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，则操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该编号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 内部版本号和发布日期](visual-studio-build-numbers-and-release-dates.md)页。

## <a name="create-an-offline-installation-folder"></a>创建脱机安装文件夹

必须具有 Internet 连接才能完成此步骤。 若要创建含所有语言和所有功能的脱机安装，请使用与下面示例相似的命令之一。

   > [!IMPORTANT]
   > 完整的 Visual Studio 布局至少需要 35 GB 磁盘空间，可能需要一段时间才能下载完成。 若要详细了解如何创建仅包含要安装的组件的布局，请参阅[自定义网络布局](#customize-the-network-layout)部分。
   >
   > [!TIP]
   > 请确保从下载目录运行该命令。 通常，在运行 Windows 10 的计算机上为：`C:\Users\<username>\Downloads`。

- 对于 Visual Studio Enterprise，请运行：

  ```vs_enterprise.exe --layout c:\VSLayout```

- 对于 Visual Studio Professional，请运行：

  ```vs_professional.exe --layout c:\VSLayout```

## <a name="modify-the-responsejson-file"></a>修改 response.json 文件

可以通过修改 response.json 来设置用户在运行安装程序时使用的默认值。  例如，可以通过配置 `response.json` 文件来选择一组自动选定的特定工作负载。 有关详细信息，请参阅[通过响应文件自动执行 Visual Studio 安装](automated-installation-with-response-file.md)。

而且，如果在将 Visual Studio 引导程序与 response.json 文件配对时遇到错误，请参阅[安装或使用 Visual Studio 时与网络相关错误的疑难解答](troubleshooting-network-related-errors-in-visual-studio.md#error-failed-to-parse-id-from-parent-process)页面的“无法从父进程分析 ID”部分，以获取有关解决方法的详细信息。

## <a name="copy-the-layout-to-a-network-share"></a>将布局复制到网络共享

在网络共享上托管布局，以便用户可以从其他计算机运行。

下面的示例使用 [xcopy](/windows-server/administration/windows-commands/xcopy/)。 如果需要，还可以使用 [robocopy](/windows-server/administration/windows-commands/robocopy/)。  

::: moniker range="vs-2017"

示例：

```cmd
xcopy /e c:\VSLayout \\server\products\VS2017
```

::: moniker-end

::: moniker range="vs-2019"

```cmd
xcopy /e c:\VSLayout \\server\products\VS2019
```

::: moniker-end

> [!IMPORTANT]
> 为了防止错误出现，请确保完整布局路径的长度小于 80 个字符。

## <a name="customize-the-network-layout"></a>自定义网络布局

可使用多个选项自定义网络布局。 可以创建仅包含一组特定[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)、[工作负载、组件及其推荐或可选依赖项](workload-and-component-ids.md)的部分布局。 如果确定只会将部分工作负载部署到客户端工作站，部分布局就非常有用。 用于自定义布局的常见命令行参数包括：

* `--add`：用于指定[工作负载或组件 ID](workload-and-component-ids.md)。 <br>如果使用 `--add`，只会下载使用 `--add` 指定的工作负载和组件。  如果不使用 `--add`，将下载所有工作负载和组件。
* `--includeRecommended`：用于添加针对指定工作负载 ID 的所有推荐组件
* `--includeOptional`：用于添加针对指定工作负载 ID 的所有推荐和可选组件。
* `--lang`：用于指定[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)。

下面的几个示例展示了如何创建自定义部分布局。

* 若要下载仅一种语言的所有工作负载和组件，请运行：

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --lang en-US
    ```

* 若要下载多种语言的所有工作负载和组件，请运行：

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --lang en-US de-DE ja-JP
    ```

* 若要下载所有语言的一个工作负载，请运行：

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* 若要下载三种语言的两个工作负载和一个可选组件，请运行：

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP
    ```

* 下载两个工作负载及其所有推荐组件：

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended
    ```

* 若要下载两个工作负载及其所有推荐和可选组件，请运行：

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional
    ```

::: moniker range="vs-2017"

### <a name="new-in-version-153"></a>15.3 版中的新增功能

::: moniker-end

::: moniker range="vs-2019"

### <a name="save-your-layout-options"></a>保存布局选项

::: moniker-end

运行布局命令时，指定的选项（例如工作负载和语言）将被保存。 后续的布局命令将包括先前的所有选项。  以下示例说明如何使用一个工作负载来创建布局（仅限英语）：

```cmd
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

若要将布局更新至较新版本，无需指定任何额外命令行参数。 此布局文件夹中的任何后续布局命令都将使用先前所保存的设置。  以下命令将更新现有的部分布局。

```cmd
vs_enterprise.exe --layout c:\VSLayout
```

有关添加其他工作负载的相关操作说明，请参阅下列示例。 在此事例中，我们将添加 Azure 工作负载和已本地化的语言。  现在，此布局中已包括托管桌面和 Azure。  所有这些工作负载中都加入了英语和德语的语言资源。 已将布局更新至最新的可用版本。

```cmd
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

要将现有布局更新至完整布局，请使用 --all 选项，如下方示例所示。

```cmd
vs_enterprise.exe --layout c:\VSLayout --all
```

## <a name="deploy-from-a-network-installation"></a>从网络安装点进行部署

管理员可以通过安装脚本将 Visual Studio 部署到客户端工作站上。 拥有管理员权限的用户也可以直接从共享运行安装程序，从而在自己的计算机上安装 Visual Studio。

* 用户可通过运行以下命令进行安装： <br>

    ```cmd
    \\server\products\VS\vs_enterprise.exe
    ```

* 管理员可以通过运行以下命令在无人参与模式下进行安装：

    ```cmd
    \\server\products\VS\vs_enterprise.exe --quiet --wait --norestart
    ```

> [!IMPORTANT]
> 为了防止错误出现，请确保完整布局路径的长度小于 80 个字符。

> [!TIP]
> 如果作为批处理文件的一部分执行，`--wait` 选项可确保 `vs_enterprise.exe` 进程先等待安装完成，再返回退出代码。
>
> 若企业管理员要在已完成的安装上执行进一步操作（例如，[向已成功的安装应用产品密钥](automatically-apply-product-keys-when-deploying-visual-studio.md)），此方法十分有用，但需要等待安装完成以处理从该安装返回的代码。
>
> 如果不使用 `--wait``vs_enterprise.exe` 进程将在安装完成前退出，并返回一个不能表示安装操作状态的不准确的退出代码。
>

::: moniker range="vs-2019"
> [!IMPORTANT]
> 对于脱机安装，如果收到一条错误消息，指出“找不到与以下参数匹配的项目”，请确保将 `--noweb` 开关用于版本 16.3.5 或更高版本。
>
::: moniker-end

从布局安装时，安装内容将从布局中获取。 但是，如果选择不在布局中的组件，则会从 Internet 获取它。  要阻止 Visual Studio 安装程序下载布局中缺少的任何内容，请使用 `--noWeb` 选项。 如果使用 `--noWeb`，但布局中缺少要安装的选定内容，安装就会失败。

> [!IMPORTANT]
> `--noWeb` 选项不会阻止 Visual Studio 安装程序检查更新。 有关详细信息，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)页。

### <a name="error-codes"></a>错误代码

如果使用 `--wait` 参数，`%ERRORLEVEL%` 环境变量会设置为下列值之一，具体视操作结果而定：

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

## <a name="update-a-network-install-layout"></a>更新网络安装布局

有产品更新时，可能需要[更新网络安装布局](update-a-network-installation-of-visual-studio.md)以纳入更新后的包。

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-release"></a>如何为旧版 Visual Studio 创建布局

::: moniker range="vs-2017"

> [!NOTE]
> 每次运行 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) 上提供的 Visual Studio 引导程序时，都会下载并安装可用的最新版 Visual Studio。
>
> 因此，如果立即下载 Visual Studio 引导程序，并从现在开始运行 6 个月，那么会安装运行引导程序时的最新 Visual Studio 版本  。
>
> 但是，如果创建布局并通过布局安装，则布局将安装布局中存在的特定 Visual Studio 版本  。 即使可能存在更高的联机版本，也只会获取布局中的 Visual Studio 版本。

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> 每次运行 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads) 上提供的 Visual Studio 引导程序时，都会下载并安装可用的最新版 Visual Studio。
>
> 因此，如果立即下载 Visual Studio 引导程序，并从现在开始运行 6 个月，那么会安装运行引导程序时的最新 Visual Studio 版本  。
>
> 但是，如果创建布局并通过布局安装，则布局将安装布局中存在的特定 Visual Studio 版本  。 即使可能存在更高的联机版本，也只会获取布局中的 Visual Studio 版本。

::: moniker-end

如需创建适合旧版 Visual Studio 的布局，可访问 [https://my.visualstudio.com](https://my.visualstudio.com)，下载“固定”版本的 Visual Studio 引导程序。

### <a name="how-to-get-support-for-your-offline-installer"></a>如何获取关于脱机安装程序的支持

如果脱机安装遇到问题，请告知我们。 告知我们的最好方式是使用[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具。 使用此工具时，可发送我们诊断和修复问题所需的遥测数据和日志。

对于安装相关问题，我们还提供[实时聊天  ](https://visualstudio.microsoft.com/vs/support/#talktous)（仅限英语）支持选项。

我们还提供其他支持选项。 若要查看列表，请参阅[反馈](../ide/feedback-options.md)页面。

## <a name="see-also"></a>请参阅

- [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
- [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
- [安装或使用 Visual Studio 时与网络相关错误的疑难解答](troubleshooting-network-related-errors-in-visual-studio.md)
- [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
- [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
- [在维修基线上更新 Visual Studio](update-servicing-baseline.md)
- [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
- [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
