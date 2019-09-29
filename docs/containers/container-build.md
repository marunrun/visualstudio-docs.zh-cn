---
title: Visual Studio 容器工具生成概述
author: ghogen
description: 容器工具生成过程概述
ms.author: ghogen
ms.date: 06/06/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: edc4674e2468124ecb46b25a1411043ed4b66a2a
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253121"
---
# <a name="building-containerized-apps-using-visual-studio-or-the-command-line"></a>使用 Visual Studio 或命令行生成容器化应用

无论是从 Visual Studio IDE 生成，还是设置命令行生成，都需要了解 Visual Studio 生成如何使用 Dockerfile 生成项目。  出于性能方面的考虑，Visual Studio 对容器化应用执行特殊的过程。 了解通过修改 Dockerfile 自定义生成过程时，Visual Studio 生成项目的特殊重要性。

Visual Studio 生成不使用 Docker 容器的项目时，它会在本地计算机上调用 MSBuild，并在本地解决方案文件夹下的文件夹（通常为 `bin`）中生成输出文件。 但是，对于容器化项目，生成过程会考虑有关生成容器化应用的 Dockerfile 说明。 Visual Studio 使用的 Dockerfile 分为多个阶段。 此过程依赖 Docker 的多阶段生成功能  。

## <a name="multistage-build"></a>多阶段生成

多阶段生成功能有助于使容器的生成过程更高效，并使容器更小，方法是让容器仅包含应用在运行时需要的位。 多阶段生成用于 .NET Core 项目，而不用于 .NET Framework 项目。

使用多阶段生成功能，可以在生成中间映像的阶段创建容器映像。 例如，请考虑 Visual Studio 生成的典型 Dockerfile - 第一阶段为 `base`：

```
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
```

Dockerfile 中的行以 Microsoft 容器注册表 (mcr.microsoft.com) 中的 Nanoserver 映像开头，并创建公开端口 80 和 443 的中间映像 `base`，并将工作目录设置为 `/app`。

下一阶段是 `build`，其显示如下：

```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["WebApplication43/WebApplication43.csproj", "WebApplication43/"]
RUN dotnet restore "WebApplication43/WebApplication43.csproj"
COPY . .
WORKDIR "/src/WebApplication43"
RUN dotnet build "WebApplication43.csproj" -c Release -o /app
```

你可以看到，`build` 阶段是从注册表（`sdk` 而不是 `aspnet`）中的其他原始映像开始，而不是从基础映像继续。  `sdk` 映像包含所有生成工具，因此，它比仅包含运行时组件的 aspnet 映像大得多。 如果看看 Dockerfile 的其余部分，你就会清楚使用单独映像的原因：

```
FROM build AS publish
RUN dotnet publish "WebApplication43.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication43.dll"]
```

最后阶段再次从 `base` 开始，并包括 `COPY --from=publish` 以将发布的输出复制到最终映像中。 由于无需包含 `sdk` 映像中的所有生成工具，因此此过程可以使最终映像小得多。

## <a name="faster-builds-for-the-debug-configuration"></a>加快调试配置的生成

Visual Studio 执行的一些优化操作有助于提高容器化项目生成过程的性能。 启动调试 (F5) 时，将重新使用以前生成的映像（如果可能）。 如果不想重复使用以前的容器，则可以在 Visual Studio 中使用“Rebuild”或“Clean”命令强制 Visual Studio 使用新的容器   。

此外，为了提高性能，容器化应用的生成过程并不像仅遵循 Dockerfile 中所述的步骤那样简单。 在容器中生成比在本地计算机上生成要慢得多。  因此，在“调试”配置中生成时，Visual Studio 实际上会在本地计算机上生成项目，然后使用卷装载将输出文件夹共享到容器  。 启用了此优化的生成称为“快速”模式生成  。

在“快速”  模式下，Visual Studio 使用参数（该参数指示 Docker 仅生成 `base` 阶段）调用 `docker build`。  Visual Studio 处理该过程的其余部分，而与 Dockerfile 的内容无关。 因此，修改 Dockerfile（例如自定义容器环境或安装其他依赖项）时，应将修改放在第一阶段。  Dockerfile 的 `build`、`publish` 或 `final` 阶段中的任何自定义步骤均不会执行。

仅当在“调试”配置中生成时才会进行此性能优化  。 在“发布”配置中，生成在 Dockerfile 中指定的容器中进行  。

如果要禁用性能优化并按 Dockerfile 指定的方式生成，请在项目文件中将“ContainerDevelopmentMode”属性设置为“常规”，如下所示   ：

```xml
<PropertyGroup>
   <ContainerDevelopmentMode>Regular</ContainerDevelopmentMode>
</PropertyGroup>
```

若要恢复性能优化，请从项目文件中删除该属性。

## <a name="building-from-the-command-line"></a>从命令行生成

可以使用 `docker build` 或 `MSBuild` 从命令行生成。

### <a name="docker-build"></a>Docker 生成

要从命令行生成容器化解决方案，通常可以对解决方案中的每个项目使用命令 `docker build <context>`。 提供生成上下文参数  。 Dockerfile 的生成上下文是本地计算机上的一个文件夹，用作生成映像的工作文件夹  。 例如，将文件复制到容器时，它是要复制的文件所在的文件夹。  在 .NET Core 项目中，请使用包含解决方案文件 (.sln) 的文件夹。  此参数表示为相对路径，对于项目文件夹中的 Dockerfile 及其父文件夹中的解决方案文件，此参数通常为“...”。  对于 .NET Framework 项目，生成上下文为项目文件夹，而不是解决方案文件夹。

```cmd
docker build -f Dockerfile ..
```

### <a name="msbuild"></a>MSBuild

由 Visual Studio for .NET Framework 项目（以及使用 Visual Studio 2017 Update 4 之前版本的 Visual Studio 版本创建的 .NET Core 项目）创建的 Dockerfile 不是多阶段 Dockerfile。  这些 Dockerfile 中的步骤不编译代码。  当 Visual Studio 生成 .NET Framework Dockerfile 时，它将首先使用 MSBuild 编译项目。  成功后，Visual Studio 会生成 Dockerfile，这只是将生成输出从 MSBuild 复制到生成的 Docker 映像中。  由于编译代码的步骤不包含在 Dockerfile 中，因此不能从命令行使用 `docker build` 生成 .NET Framework Dockerfile。 应使用 MSBuild 生成这些项目。

要为单个 Docker 容器项目生成映像，可以将 MSBuild 与 `/t:ContainerBuild` 命令选项一起使用。 例如:

```cmd
MSBuild MyProject.csproj /t:ContainerBuild /p:Configuration=Release
```

从 Visual Studio IDE 生成解决方案时，你将看到类似于在“输出”窗口中看到的输出  。 始终使用 `/p:Configuration=Release`，因为在 Visual Studio 使用多阶段生成优化的情况下，生成“调试”配置时产生的结果可能与预期不符  。

如果使用的是 Docker Compose 项目，请使用命令生成映像：

```cmd
msbuild /p:SolutionPath=<solution-name>.sln /p:Configuration=Release docker-compose.dcproj
```

## <a name="next-steps"></a>后续步骤

了解如何通过在项目文件中设置其他 MSBuild 属性来进一步自定义生成。 请参阅[容器项目的 MSBuild 属性](container-msbuild-properties.md)。

## <a name="see-also"></a>请参阅

[MSBuild](../msbuild/msbuild.md)
[Windows 上的 Dockerfile ](/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile)
[Windows 上的 Linux 容器](/virtualization/windowscontainers/deploy-containers/linux-containers)
