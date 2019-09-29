---
title: 对容器化应用进行单元测试
author: ghogen
description: 在 Visual Studio 中对 Docker 项目的每个生成运行单元测试
ms.author: ghogen
ms.date: 06/17/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: ec5aea44362cf82f6745671cc0706f80e01a60ad
ms.sourcegitcommit: 0cd282a7584b9bfd4df7882f8fdf3ad8a270e219
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "71125967"
---
# <a name="how-to-run-unit-tests-for-a-containerized-app"></a>如何：为容器化应用运行单元测试

可以通过修改 Dockerfile 来对容器化项目的每个生成运行单元测试。

## <a name="prerequisites"></a>系统必备

- [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- 安装 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)
- 单元测试设置为使用 [dotnet 测试](/dotnet/core/tools/dotnet-test)运行
- 安装[容器窗口扩展](https://aka.ms/vscontainerspreview)

## <a name="add-unit-tests-to-the-dockerfile"></a>向 Dockerfile 添加单元测试

在修改 Dockerfile 之前，Visual Studio 会执行一些特殊的性能优化。 生成“调试”配置时，Visual Studio 将在本地计算机上生成项目，并将结果复制到容器  。 因此，只会按照 Dockerfile 中指定的方式执行多阶段 Dockerfile 的第一阶段。 有关详细信息，请参阅[适用于 Visual Studio 的容器工具生成过程](container-build.md)。

若要将单元测试添加到多阶段 Dockerfile，请在 `build` 和 `publish` 阶段之间将 `unit-test` 阶段添加到 Dockerfile。

```
FROM build AS unit-test
RUN dotnet unit-test --logger:trx
```

Visual Studio 仅在“调试”配置中运行第一个阶段，因此 `unit-test` 阶段仅在“发布”配置中运行   。 即使在“发布”配置中，日志结果也不会包含在最终映像中，因为最终映像是从 `base` 阶段而不是从 `unit-test` 阶段生成的  。 若要运行测试并生成可以在其中查看日志的映像，请使用以下命令：

```cmd
docker build --target:unit-test
```

## <a name="next-steps"></a>后续步骤

然后可以使用[容器窗口](view-and-diagnose-containers.md)（若已安装扩展）来查看测试日志。  

若要查看测试日志，请使用 Ctrl+Q 并搜索“容器”以打开“容器”窗口     。 在“容器”窗口中，找到自己的容器，打开“文件”选项卡，在容器的文件系统中查找测试结果 (.trx) 文件，然后打开该文件，在 Visual Studio 中查看结果   。

