---
title: 使用最小脱机布局更新 Visual Studio
description: 了解如何使用最小脱机布局更新 Visual Studio。
ms.date: 07/21/2020
ms.custom: seodec18
ms.topic: how-to
ms.assetid: ''
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 2b9c86c17b89258145613e867ba6a91b2219fe0d
ms.sourcegitcommit: 2c26d6e6f2a5c56ae5102cdded7b02f2d0fd686c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88168744"
---
# <a name="update-visual-studio-using-a-minimal-offline-layout"></a>使用最小脱机布局更新 Visual Studio

对于未连接到 Internet 的计算机，创建最小布局是更新脱机 Visual Studio 实例的最简单、最快捷的方法。

最小布局工具可根据团队需求生成特别定制的布局。 企业管理员可使用此工具为 Visual Studio 2017 和 2019 的大多数版本创建更新布局。 与完整的 Visual Studio 布局不同，最小布局只包含更新的包，因此它总是更小，生成和部署速度也更快。 仅指定所需语言、工作负载和组件，可进一步缩小更新布局。

## <a name="how-to-generate-a-minimal-layout"></a>如何生成最小布局

> [!IMPORTANT]
> 这些说明假定你之前已创建和使用布局。 要详细了解如何执行此操作，请参阅[更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)页面。
>
> 若要详细了解 Visual Studio 生命周期，请参阅 [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing)页面。
>

此工具为 Visual Studio 2017 (15.9) 及更高版本创建更新布局。 可将布局部署到网络/脱机计算机以更新 Visual Studio 实例。 在[普通布局创建](update-a-network-installation-of-visual-studio.md)期间，将下载该特定版本的所有包。 在 Visual Studio 实例上执行修复、卸载和其他标准操作时，需要创建普通布局。 最小布局仅下载更新的包，因此它更小且更易于复制到脱机计算机。

### <a name="installing-the-minimal-layout-tool"></a>安装最小布局工具
 
 1. 首先，下载[此处](https://aka.ms/vs/installer/minimallayout)的最小布局工具。 在出现提示时，确保依次选择“保存”、“运行” 。

     ![保存最小布局工具](media/save-minimal-layout.png)

 2. 接下来，单击“是”以接受用户帐户控制提示。

     ![接受用户帐户控制](media/accept-user-account-control.png)

 3. 最小布局工具将安装到 `C:\Program Files (x86)\Microsoft Visual Studio\MinimalLayout`。

### <a name="how-to-use-the-minimal-layout-tool"></a>如何使用最小布局工具

`MinimalLayout.exe` 使用以下命令和选项生成布局。 至少需要一个命令来运行该工具。 以下是运行该工具的方法：

```MinimalLayout.exe [command] <options>...```

#### <a name="commands"></a>命令
* **预览**：使用此命令可预览将下载的包数以及用于创建此布局的总空间。 
* **Generate**：使用此命令可生成用于更新 Visual Studio 的最小布局。
* **Regenerate**：使用此命令可使用现有的最小布局响应文件再生成布局。 每个最小布局都会生成一个 `MinimalLayout.json` 响应文件，其中包含原始的最小布局输入参数。 你可使用 Regenerate 命令和 `MinimalLayout.json` 响应文件来再生成最小布局。 如果要基于之前的最小布局的响应文件为新的 Visual Studio 更新创建最小布局，这会很有用。

   对于此命令，需要已生成的布局中的 `MinimalLayout.json` 文件路径。 

    ```cmd
    MinimalLayout.exe regenerate --filePath C:\MinimalLayout\MinimalLayout.json
    ```

* **Verify**：使用此命令可确定布局文件夹是否已损坏。
* **Fix**：使用此命令可修复损坏的布局文件夹，包括替换布局文件夹中缺少的任何包。

#### <a name="options"></a>选项 

|选项    |说明    |必需/可选 |示例 |
|:----------|:-----------|:------------|:--------------|
|--targetLocation &lt;dir&gt; |指定要在其中创建最小脱机布局的目录。       |必需        |--targetLocation c:\VSLayout\ |
|--baseVersion &lt;version&gt;|从此版本开始，将生成最小脱机布局。   |必需|--baseVersion 16.4.0 |
|--targetVersion &lt;version&gt;|此版本及以下版本，将生成最小脱机布局。|必需|--targetVersion 16.4.4|
|--languages    |指定要包含在最小脱机布局中的语言。 可指定多个值，并用空格分隔。    |必需    |--languages en-US fr-FR |
|--productId &lt;id&gt;    |将从中生成最小脱机布局的产品的 ID。 <br> <ul><li>Microsoft.VisualStudio.Product.Enterprise</li><li>Microsoft.VisualStudio.Product.Professional</li><li>Microsoft.VisualStudio.Product.BuildTools</li><li>Microsoft.VisualStudio.Product.TestAgent</li><li>Microsoft.VisualStudio.Product.TestController</li><li>Microsoft.VisualStudio.Product.TeamExplorer</li></ul>|必需|--productId Microsoft.VisualStudio.Product.Enterprise |
|--filePath    |已创建的布局中的 MinimalLayout.json 文件的文件路径。 此选项仅与 Regenerate 命令一起使用。     |Regenerate 命令所需内容    |--filePath C:\VSLayout\minimalLayout.json <br><br> 请注意，Regenerate 命令只使用 --filePath 作为选项。 |
|--add &lt;一个或多个工作负载或组件 ID&gt;    |指定要添加的一个或多个工作负载或组件 ID。 可以使用 --includeRecommended 和/或 –-includeOptional 全局添加 <br> 额外的组件。 可以指定多个工作负载或组件 ID，用空格分隔。    |可选    |--add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb Component.GitHub.VisualStudio |
|--includeRecommended    |包含所有已安装工作负载的推荐组件，但不包含可选组件。    |可选    |对于特定工作负载： <br> --add Microsoft.VisualStudio.Workload. ManagedDesktop;includeRecommended <br><br> 应用于所有工作负载：--includeRecommended |
|--includeOptional |包含所有已安装工作负载的可选组件，包括建议组件。    |可选    |对于特定工作负载： <br>--add Microsoft.VisualStudio.Workload. ManagedDesktop;includeOptional <br><br> 应用于所有工作负载：--includeOptional |

### <a name="generating-a-minimal-layout"></a>生成最小布局

> [!IMPORTANT]
>  这些说明假定你之前已创建了一个网络安装布局。 要详细了解如何执行此操作，请参阅[创建 Visual Studio 的网络安装](create-a-network-installation-of-visual-studio.md)页面。

使用 generate 命令为指定的版本范围创建最小布局。 还需要了解 productId、语言以及所需的任何特定工作负载。 这一最小布局会将任何 Visual Studio 实例从基础版本更新到包含目标版本。

创建布局之前，可以使用 preview 命令了解下载总大小以及所包含的包数。 此命令采用与 generate 命令相同的选项，将详细信息写入控制台。

让我们通过几个示例来演示如何预览、生成和再生成最小布局：

- 首先，以下示例演示如何预览 Visual Studio Enterprise 版本 16.4.0 到 16.4.4 的布局（仅限英文）。

    ```cmd
    MinimalLayout.exe preview --targetLocation c:\VSLayout\ --productId Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --languages en-US
    ```

- 下面介绍如何使用一个工作负载生成相同布局。

    ```cmd
    MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productId Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US
    ```

- 下面介绍如何使用现有响应文件再生成最小脱机布局。 

    ```cmd
    MinimalLayout.exe regenerate -filepath c:\VSLayout\MinimalLayout.json
    ```

使用 generate 命令的几个其他示例：

- 下面介绍如何添加附加工作负载，并仅包含推荐的包。 

    ```cmd
    MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productId Microsoft.VisualStudio.Product.Professional --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop Microsoft.VisualStudio.Workload.NetWeb;includeRecommended --languages en-US
    ```

- 最后，这里介绍如何在最小布局中包含多种语言。 

    ```cmd
    MinimalLayout.exe generate --targetLocation c:\VSLayout\ --productId Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeOptional --languages en-US fr-FR
    ```

### <a name="how-to-maintain-a-minimal-layout"></a>如何维护最小布局

使用 verify 和 fix 命令，在创建最小布局后维护它 。 verify 命令确定最小布局中是否存在任何损坏或缺少的包。 如果运行 verify 命令后遇到任何问题，请使用 fix 命令更正那些缺少或损坏的包 。

- 下面介绍如何验证布局是否存在损坏或缺少的包： 

    ```cmd
    MinimalLayout.exe Verify --targetLocation c:\VSLayout\ --productId Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --languages en-US
    ```

- 下面介绍如何修复此布局：

    ```cmd
    MinimalLayout.exe fix --targetLocation C:\VSLayout\ --productId Microsoft.VisualStudio.Product.Enterprise --baseVersion 16.4.0 --targetVersion 16.4.4 --add Microsoft.VisualStudio.Workload.ManagedDesktop;includeRecommended --languages en-US
    ```

>[!NOTE] 
> 此布局不能用于修复 Visual Studio 安装。 若要修复 Visual Studio 的现有实例，请参阅[修复 Visual Studio](repair-visual-studio.md)。
>

### <a name="how-to-use-a-minimal-offline-layout-to-update-an-existing-installation-of-visual-studio"></a>如何使用最小脱机布局更新 Visual Studio 的现有安装

生成最小布局后，可以将整个最小布局文件夹复制到客户端计算机。 如果计算机无法访问其原始位置的最小布局文件夹，则需要执行此操作。

导航到该文件夹并标识引导程序应用程序名称。 引导程序应用程序的名称取决于生成最小布局时指定的 ProductId 值。 有关常见示例，请参阅下表。

|ProductId 值    |应用程序名称|
|:-----------|:------------|
|Microsoft.VisualStudio.Product.Enterprise    |vs_enterprise.exe|
|Microsoft.VisualStudio.Product.Professional    |vs_professional.exe|
|Microsoft.VisualStudio.Product.BuildTools    |vs_buildtools.exe|

只需两个步骤即可将更新应用于 Visual Studio 实例。 首先更新 Visual Studio 安装程序，然后更新 Visual Studio。

1. **更新 Visual Studio 安装程序** 

    运行以下命令，将 `vs_enterprise.exe` 替换为正确的引导程序应用程序名称（如有必要）。 

    ```cmd
    vs_enterprise.exe --quiet --update --offline C:\VSLayout\vs_installer.opc
    ```

2. **更新 Visual Studio 应用程序**

    若要更新 Visual Studio，需要指定要更新的 Visual Studio 实例的 installPath。 如果安装了多个 Visual Studio 实例，则需要单独更新每个实例。 强烈建议使用 update 命令指定 `–noWeb` 选项，以防止安装不在最小布局中的组件。 这可以防止 Visual Studio 处于不可用状态。

    运行以下命令，并适当地替换 installPath 命令行参数。 请务必使用正确的引导程序应用程序名称。

    ```cmd
    vs_enterprise.exe update --noWeb --quiet --installpath "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise"
    ```

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [如何在响应文件中定义设置](automated-installation-with-response-file.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
