---
title: Visual Studio 容器工具 Docker Compose 生成设置
author: ghogen
description: 容器工具生成过程概述
ms.author: ghogen
ms.date: 08/12/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: 2178881c6ea0e597aef5e25074e3648162d3f6e9
ms.sourcegitcommit: 6ae0a289f1654dec63b412bfa22035511a2ef5ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71950641"
---
# <a name="docker-compose-build-properties"></a>Docker Compose 生成属性

除了用于控制各个 Docker 项目的属性（如[容器工具生成属性](container-msbuild-properties.md)中所述），还可以通过设置 MSBuild 用于生成解决方案的 Docker Compose 属性来自定义 Visual Studio 生成 Docker Compose 项目的方式。 还可以通过设置 Docker Compose 配置文件中的文件标签来控制 Visual Studio 调试程序运行 Docker Compose 应用的方式。

## <a name="how-to-set-the-msbuild-properties"></a>如何设置 MSBuild 属性

若要设置属性的值，请编辑项目文件。 对于 Docker Compose 属性，此项目文件是扩展名为 .dcproj 的文件，除非在下一部分的表中另有说明。 例如，假设要指定在开始调试时启动浏览器。 可以在 .dcproj 项目文件中设置 `DockerLaunchAction` 属性，如下所示。

```xml
<PropertyGroup>
   <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
</PropertyGroup>
```

可以向现有 `PropertyGroup` 元素添加属性设置，如果没有，则新建一个 `PropertyGroup` 元素。

## <a name="docker-compose-msbuild-properties"></a>Docker Compose MSBuild 属性

下表显示了可用于 Docker Compose 项目的 MSBuild 属性。

| 属性名称 | 位置 | 说明 | 默认值  |
|---------------|----------|-------------|----------------|
|DockerComposeBuildArguments|dcproj|指定要传递给 `docker-compose build` 命令的额外参数。 例如，`--parallel --pull` |
|DockerComposeDownArguments|dcproj|指定要传递给 `docker-compose down` 命令的额外参数。 例如，`--timeout 500`|-|  
|DockerComposeProjectPath|csproj 或 vbproj|Docker-compose 项目 (.dcproj) 文件的相对路径。 发布服务项目时设置此属性，以查找存储在 docker-compose.yml 文件中的关联映像生成设置。|-|
|DockerComposeUpArguments|dcproj|指定要传递给 `docker-compose up` 命令的额外参数。 例如，`--timeout 500`|-|
|DockerLaunchAction| dcproj | 指定要针对 F5 或 Ctrl+F5 执行的启动操作。  允许的值为 None、LaunchBrowser 和 LaunchWCFTestClient|无|
|DockerLaunchBrowser| dcproj | 指示是否启动浏览器。 如果指定了 DockerLaunchAction，则忽略。 | False |
|DockerServiceName| dcproj|如果指定了 DockerLaunchAction 或 DockerLaunchBrowser，则 DockerServiceName 为应启动的服务名称。  使用此属性来确定将启动 docker-compose 文件可能引用的多个项目中的哪一个。|-|
|DockerServiceUrl| dcproj | 启动浏览器时将使用的 URL。  有效的替换令牌为“{ServiceIPAddress}”、“{ServicePort}”和“{Scheme}”。  例如：{Scheme}://{ServiceIPAddress}:{ServicePort}|-|
|DockerTargetOS| dcproj | 生成 Docker 映像时使用的目标 OS。|-|

> [!NOTE]
> DockerComposeBuildArguments、DockerComposeDownArguments 和 DockerComposeUpArguments 是 Visual Studio 2019 版本 16.3 中的新增内容。

## <a name="docker-compose-file-labels"></a>Docker Compose 文件标签

还可以将名为 docker-compose.yml（对于“调试”配置）或 docker-compose.override.yml（对于“发布”配置）的文件放在与 docker-compose.yml 文件相同的目录中，从而替代特定设置      。  可以在此文件中指定如下所示的设置：

```yml
services:
  webapplication1:
    labels:
      com.microsoft.visualstudio.debuggee.workingdirectory: "C:\\my_app_folder"
```

如前面的示例所示，用双引号将这些值括起来，并在路径中使用反斜杠作为转义字符。

|标签名称|说明|
|----------|-----------|
|com.microsoft.visualstudio.debuggee.arguments|开始调试时传递给程序的参数。 对于 .NET Core 应用，这些参数通常是 NuGet 包的其他搜索路径，后面是指向项目输出程序集的路径。|
|com.microsoft.visualstudio.debuggee.killprogram|此命令用于停止在容器中运行的调试对象程序（如有必要）。|
|com.microsoft.visualstudio.debuggee.program|启动调试时启动的程序。 对于 .Net Core 应用，此设置通常为“dotnet”  。|
|com.microsoft.visualstudio.debuggee.workingdirectory|开始调试时用作起始目录的目录。 对于 Linux 容器，此设置通常为 /app；对于 Windows 容器，此设置通常为 C:\app   。|

## <a name="next-steps"></a>后续步骤

有关 MSBuild 属性的一般信息，请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="see-also"></a>请参阅

[容器工具生成属性](container-msbuild-properties.md)

[容器工具启动设置](container-launch-settings.md)

[MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)
