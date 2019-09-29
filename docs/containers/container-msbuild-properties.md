---
title: Visual Studio 容器工具生成属性
author: ghogen
description: 容器工具生成过程概述
ms.author: ghogen
ms.date: 06/06/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: 4bc6cb4221d85bd43b98b2ac36c34c919937960b
ms.sourcegitcommit: 3cda0d58c5cf1985122b8977b33a171c7359f324
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "71126057"
---
# <a name="container-tools-build-properties"></a>容器工具生成属性

可通过设置 MSBuild 用于生成项目的属性来自定义 Visual Studio 生成容器项目的方式。 例如，可以更改 Dockerfile 的名称，指定映像的标记和标签，提供传递给 Docker 命令的其他参数，并控制 Visual Studio 是否执行某些性能优化，如在容器环境外生成。 还可以设置调试属性（如要启动的可执行文件的名称），以及要提供的命令行参数。

若要设置属性的值，请编辑项目文件。 例如，假设 Dockerfile 名为 MyDockerfile  。 可在项目文件中设置 `DockerfileFile` 属性，如下所示。

```xml
<PropertyGroup>
   <DockerfileFile>MyDockerfile</DockerfileFile>
</PropertyGroup>
```

可以向现有 `PropertyGroup` 元素添加属性设置，如果没有，则新建一个 `PropertyGroup` 元素。

下表显示可用于容器项目的 MSBuild 属性。

| 属性名称 | 说明 | 默认值  |
|---------------|-------------|----------------|
| DockerfileFile | 描述用于生成/运行项目容器的默认 Dockerfile。 此属性也可以是路径。 | Dockerfile |
| DockerfileTag | 生成 Docker 映像时使用的标记。 在调试过程中，将“:dev”追加到标记中。 | 使用以下规则去除非字母数字字符后的程序集名称： <br/> 如果生成的标记全部为数值，则将“image”作为前缀插入（例如 image2314） <br/> 如果生成的标记为空字符串，则将“image”用作标记。 |
| DockerContext | 生成 Docker 映像时使用的默认上下文。 | 由 Visual Studio 设置。 |
| ContainerDevelopmentMode | 控制是否启用“build-on-host”优化（“快速模式”调试）。  允许的值为“快速”和“常规”   。 | 快速 |
| DockerDefaultTargetOS | 生成 Docker 映像时使用的默认目标操作系统。 | 由 Visual Studio 设置。 |
| DockerImageLabels | 应用于 Docker 映像的默认标签集。 | com.microsoft.created-by=visual-studio;com.microsoft.visual-studio.project-name=$(MSBuildProjectName) |
| ContainerVsDbgPath | VSDBG 调试器的路径。 | `%USERPROFILE%\vsdbg\vs2017u5` |
| DockerfileBuildArguments | 传递给 Docker 生成命令的其他参数。 | 不适用。 |
| DockerfileRunArguments | 传递给 Docker 运行命令的其他参数。 | 不适用。 |
| DockerfileRunEnvironmentFiles | Docker 运行过程中应用的以分号分隔的环境文件列表。 | 不适用。 |
| DockerfileFastModeStage | 在调试模式下生成图像时要使用的 Dockerfile 阶段（即目标）。 | 在 Dockerfile 中找到的第一阶段（基本） |
| DockerDebuggeeProgram | 调试时，指示调试器启动此可执行文件。 | 对于 .NET Core 项目：dotnet、ASP.NET .NET Framework 项目：不适用（始终使用 IIS） |
| DockerDebuggeeArguments | 调试时，指示调试器将这些参数传递给已启动的可执行文件。 | 不适用于 ASP.NET .NET Framework 项目 |
| DockerDebuggeeWorkingDirectory | 调试时，指示调试器使用此路径作为工作目录。 | C:\app (Windows) 或 /app (Linux) |
| DockerDebuggeeKillProgram | 此命令用于在容器中终止正在运行的进程。 | 不适用于 ASP.NET .NET Framework 项目 |

## <a name="next-steps"></a>后续步骤

有关 MSBuild 属性的一般信息，请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="see-also"></a>请参阅

[Docker Compose 生成属性](docker-compose-properties.md)

[容器工具启动设置](container-launch-settings.md)

[MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)
