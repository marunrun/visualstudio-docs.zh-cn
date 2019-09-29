---
title: 配置 Visual Studio 容器工具
description: 配置 Visual Studio 中可用的工具以使用 Docker 容器。
author: ghogen
ms.author: ghogen
ms.topic: conceptual
ms.date: 03/20/2019
ms.technology: vs-azure
ms.openlocfilehash: f05eb5d92c0cdaa1242f0d98c3d877eebae27bb1
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253150"
---
# <a name="how-to-configure-visual-studio-container-tools"></a>如何配置 Visual Studio 容器工具

使用 Visual Studio 设置，可以控制将 Visual Studio 与 Docker 容器结合使用的一些方面，包括在使用 Docker 容器时影响性能和资源使用情况的设置。

## <a name="container-tools-settings"></a>容器工具设置

从主菜单中，选择“工具”>“选项”，然后展开“容器工具”>“设置”   。 随即出现容器工具设置。

::: moniker range="vs-2017"

![Visual Studio 容器工具选项，其中显示：“在项目加载时自动拉取所需的 Docker 映像”、“在后台自动启动容器”、“在解决方案关闭时自动终止容器”以及“不提示需要信任 SSL 证书”。](./media/overview/visual-studio-docker-tools-options.png)
::: moniker-end

::: moniker range=">=vs-2019"

容器工具常规设置  ：

![Visual Studio 容器工具选项，其中显示：如有需要，请安装 Docker Desktop，并信任 ASP.NET Core SSL 证书。](./media/configure-container-tools/tools-options-1.png)

容器工具“单个项目”和“Docker Compose”设置   ：

![Visual Studio 容器工具选项，其中显示：在项目关闭时终止容器，在项目打开时拉取所需的 Docker 映像，并在项目打开时运行容器。](./media/configure-container-tools/tools-options-2.png)
::: moniker-end

下表可帮助确定如何设置这些选项。

::: moniker range="vs-2017"
| name | 默认设置 | 适用于 | 说明 |
| -----|:---------------:|:----------:| ----------- |
| 在项目加载时自动拉取所需的 Docker 映像 | On | Docker Compose | 为了在加载项目时提高性能，Visual Studio 将在后台启动 Docker 拉取操作，以便在准备好运行代码时，映像已下载或正在下载。 如果只需加载项目和浏览代码，可以将其关闭，以避免下载不需要的容器映像。 |
| 在后台自动启动容器 | On | Docker Compose | 同样，为了提高性能，Visual Studio 会在构建和运行容器时创建卷装载随时可用的容器。 如果要控制创建容器的时间，请将其关闭。 |
| 在解决方案关闭时自动终止容器 | On | Docker Compose | 如果希望解决方案的容器在关闭解决方案或关闭 Visual Studio 后继续运行，请将其关闭。 |
| 不提示需要信任 localhost SSL 证书 | Off | ASP.NET Core 2.1 项目 | 如果 localhost SSL 证书不受信任，则每次运行项目时 Visual Studio 都会提示，除非选中此复选框。 |
::: moniker-end

::: moniker range=">=vs-2019"

下表描述了“常规”设置  ：

| name | 默认设置 | 适用于 | 说明 |
| -----|:---------------:|:----------:| ----------- |
| 根据需要安装 Docker Desktop | 提醒我 | 单个项目、Docker Compose | 选择是否需要在未安装 Docker Desktop 时提醒你。 |
| 信任 ASP.NET Core SSL 证书 | 提醒我 | ASP.NET Core 2.x 项目 | 设置为“提醒我”后，如果 localhost SSL 证书不受信任，则 Visual Studio 将在每次运行项目时提示你  。 |

下表描述了“单个项目”和“Docker Compose”设置   ：

| name | 默认设置 | 适用于 | 说明 |
| -----|:---------------:|:----------:| ----------- |
| 在项目打开时拉取所需的 Docker 映像 | True | 单个项目、Docker Compose | 为了在加载项目时提高性能，Visual Studio 将在后台启动 Docker 拉取操作，以便在准备好运行代码时，映像已下载或正在下载。 如果只需加载项目和浏览代码，可以将其设置为“False”，以避免下载不需要的容器映像  。 |
| 在项目打开时运行容器 | True | 单个项目、Docker Compose | 同样，为了提高性能，Visual Studio 会提前创建一个容器，以便在构建和运行容器时随时可使用该容器。 如果要控制创建容器的时间，请将其设置为“False”  。 |
| 在项目关闭时停止容器 | True | 单个项目和 Docker Compose | 如果希望解决方案的容器在关闭解决方案或关闭 Visual Studio 后继续运行，请将其设置为“False”  。 |

::: moniker-end
> [!WARNING]
> 如果 localhost SSL 证书不受信任且选中该框以禁止出现提示，则 HTTPS Web 请求可能会在应用或服务中在运行时失败。 在这种情况下，请取消选中“不提示”复选框，运行项目并在提示时指示信任  。

## <a name="next-steps"></a>后续步骤

通过此[概述](visual-studio-tools-for-docker.md)详细了解如何使用 Visual Studio 中的容器。