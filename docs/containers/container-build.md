---
title: Visual Studio 容器工具生成和调试概述
author: ghogen
description: 容器工具生成和调试过程概述
ms.author: ghogen
ms.date: 11/20/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: e1b2f332563503dcb4d63faf301000db83eed5ea
ms.sourcegitcommit: 49ebf69986713e440fd138fb949f1c0f47223f23
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74706824"
---
# <a name="how-visual-studio-builds-containerized-apps"></a>Visual Studio 如何构建容器化应用

无论是从 Visual Studio IDE 生成，还是设置命令行生成，都需要了解 Visual Studio 如何使用 Dockerfile 生成项目。  出于性能方面的考虑，Visual Studio 对容器化应用执行特殊的过程。 了解通过修改 Dockerfile 自定义生成过程时，Visual Studio 生成项目的特殊重要性。

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

Dockerfile 中的行以 Microsoft 容器注册表 (mcr.microsoft.com) 中的 Nano Server 映像开头，并创建公开端口 80 和 443 的中间映像 `base`，并将工作目录设置为 `/app`。

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

## <a name="building-from-the-command-line"></a>从命令行生成

如果要在 Visual Studio 外进行生成，可以使用 `docker build` 或 `MSBuild` 从命令行生成。

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

从 Visual Studio IDE 生成解决方案时，你将看到类似于在“输出”窗口中看到的输出  。 始终使用 `/p:Configuration=Release`，因为在 Visual Studio 使用多阶段生成优化的情况下，生成“调试”配置时产生的结果可能与预期不符  。 请参阅[调试](#debugging)。

如果使用的是 Docker Compose 项目，请使用此命令生成映像：

```cmd
msbuild /p:SolutionPath=<solution-name>.sln /p:Configuration=Release docker-compose.dcproj
```

## <a name="project-warmup"></a>项目预热

项目预热指的是在为项目选择 Docker 配置文件时（即在加载项目或添加 Docker 支持时）执行的一系列步骤，旨在提高后续运行的性能（F5 或 Ctrl+F5）     。 在“工具” > “选项” > “容器工具”下可以配置项目预热    。 下面是在后台运行的任务：

- 检查 Docker Desktop 是否已安装且正在运行。
- 确保将 Docker Desktop 设置为与项目相同的操作系统。
- 在 Dockerfile 的第一阶段（大部分 Dockerfile 中的 `base` 阶段）拉取映像。  
- 生成 Dockerfile 并启动容器。

预热仅在快速模式下进行，因此正在运行的容器将装载应用文件夹卷  。 这意味着对应用所做的任何更改都不会使容器无效。 因此可以大幅提升调试性能，并缩短长期任务（例如拉取大型映像）的等待时间。

## <a name="volume-mapping"></a>卷映射

为了能够在容器中正常调试，Visual Studio 使用卷映射从主机映射调试程序和 NuGet 文件夹。 下面是在容器中装载的卷：

|||
|-|-|
| **远程调试程序** | 包含在容器中运行调试器所需的位，视具体项目类型而定。 有关详细信息， |请参阅[调试](#debugging)部分。
| **应用文件夹** | 包含 Dockerfile 所在的项目文件夹。|
| **源文件夹** | 包含传递给 Docker 命令的生成上下文。|
| **NuGet 包文件夹** | 包含从项目的 obj\{project}.csproj.nuget.g.props 文件中读取的 NuGet 包和 fallback 文件夹  。 |

对于 ASP.NET Core Web 应用，SSL 证书和用户机密可能还有两个额外的文件夹，下一部分将对此进行详细介绍。

## <a name="ssl-enabled-aspnet-core-apps"></a>启用 SSL 的 ASP.NET Core 应用

Visual Studio 中的容器工具支持使用开发证书调试启用 SSL 的 ASP.NET Core 应用，调试方式与在没有容器的情况下相同。 为实现此目的，Visual Studio 会添加几个步骤来导出证书，使其可供容器使用。 流程如下：

1. 通过 `dev-certs` 工具，确保主机上存在本地开发证书且该证书受主机信任。
2. 将该证书导出到 %APPDATA%\ASP.NET\Https，并将安全密码存储在此特定应用的用户机密存储中。
3. 卷装载以下目录：

   -  %APPDATA%\Microsoft\UserSecrets
   -  %APPDATA%\ASP.NET\Https

ASP.NET Core 将查找与 Https 文件夹下的程序集名称匹配的证书，这就是将其映射到该路径中的容器的原因  。 还可以使用环境变量（即 `ASPNETCORE_Kestrel__Certificates__Default__Path` 和 `ASPNETCORE_Kestrel__Certificates__Default__Password`）或在用户机密 json 文件中定义证书路径和密码，例如：

```json
{
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "c:\\app\\mycert.pfx",
        "Password": "strongpassword"
      }
    }
  }
}
```

要详细了解如何将 SSL 与容器中的 ASP.NET Core 应用结合使用，请参阅 [Hosting ASP.NET Core images with Docker over HTTPS](https://docs.microsoft.com/aspnet/core/security/docker-https)（通过 HTTPS 使用 Docker 托管 ASP.NET Core 映像）。

## <a name="debugging"></a>调试

在调试配置中进行生成时，Visual Studio 执行的一些优化操作有助于提高容器化项目生成过程的性能  。 容器化应用的生成过程并不像仅遵循 Dockerfile 中所述的步骤那样简单。 在容器中生成比在本地计算机上生成要慢得多。  因此，在“调试”配置中生成时，Visual Studio 实际上会在本地计算机上生成项目，然后使用卷装载将输出文件夹共享到容器  。 启用了此优化的生成称为“快速”模式生成  。

在“快速”  模式下，Visual Studio 使用参数（该参数指示 Docker 仅生成 `base` 阶段）调用 `docker build`。  Visual Studio 处理该过程的其余部分，而与 Dockerfile 的内容无关。 因此，修改 Dockerfile（例如自定义容器环境或安装其他依赖项）时，应将修改放在第一阶段。  Dockerfile 的 `build`、`publish` 或 `final` 阶段中的任何自定义步骤均不会执行。

仅当在“调试”配置中生成时才会进行此性能优化  。 在“发布”配置中，生成在 Dockerfile 中指定的容器中进行  。

如果要禁用性能优化并按 Dockerfile 指定的方式生成，请在项目文件中将“ContainerDevelopmentMode”属性设置为“常规”，如下所示   ：

```xml
<PropertyGroup>
   <ContainerDevelopmentMode>Regular</ContainerDevelopmentMode>
</PropertyGroup>
```

若要恢复性能优化，请从项目文件中删除该属性。

 启动调试 (F5) 时，将重新使用以前启动的容器（如有）  。 如果不想重复使用以前的容器，则可以在 Visual Studio 中使用“Rebuild”或“Clean”命令强制 Visual Studio 使用新的容器   。

运行调试程序的过程取决于项目类型和容器操作系统：

|||
|-|-|
| **.NET Core 应用（Linux 容器）**| Visual Studio 下载 `vsdbg` 并将其映射到容器，然后通过程序和参数（即 `dotnet webapp.dll`）进行调用，接着调试程序附加到进程中。 |
| **.NET Core 应用（Windows 容器）**| Visual Studio 使用 `onecoremsvsmon` 并将其映射到容器，将其作为入口点运行，然后 Visual Studio 与其建立连接并附加到程序中。 此过程与通常在其他计算机或虚拟机上设置远程调试的过程类似。|
| **.NET Framework 应用** | Visual Studio 使用 `msvsmon` 并将其映射到容器，将其作为入口点（Visual Studio 可通过此入口点与其建立连接）的一部分运行，并附加到程序中。|

有关 `vsdbg.exe` 的信息，请参阅[通过 Visual Studio 对 Linux 和 OSX 上的 .NET Core 进行 Offroad 调试](https://github.com/Microsoft/MIEngine/wiki/Offroad-Debugging-of-.NET-Core-on-Linux---OSX-from-Visual-Studio)。

## <a name="container-entry-point"></a>容器入口点

Visual Studio 使用自定义容器入口点，具体视项目类型和容器操作系统而定，下面是不同的组合：

|||
|-|-|
| **Linux 容器** | 入口点为 `tail -f /dev/null`，表示无限等待，可使容器保持运行。 当应用通过调试程序启动时，调试程序会负责运行应用（即 `dotnet webapp.dll`）。 如果在不进行调试的情况下启动，则该工具将运行 `docker exec -i {containerId} dotnet webapp.dll` 以运行应用。|
| **Windows 容器**| 入口点类似于用于运行调试程序的 `C:\remote_debugger\x64\msvsmon.exe /noauth /anyuser /silent /nostatus`，因此它侦听连接。 同样地，如果在不进行调试的情况下启动，调试程序会运行应用和 `docker exec` 命令。 对于 .NET Framework Web 应用，入口点略有不同，会向命令添加 `ServiceMonitor`。|

容器入口点只能在 docker-compose 项目中修改，而不能在单个容器项目中修改。

## <a name="next-steps"></a>后续步骤

了解如何通过在项目文件中设置其他 MSBuild 属性来进一步自定义生成。 请参阅[容器项目的 MSBuild 属性](container-msbuild-properties.md)。

## <a name="see-also"></a>请参阅

[MSBuild](../msbuild/msbuild.md)
[Windows 上的 Dockerfile ](/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile)
[Windows 上的 Linux 容器](/virtualization/windowscontainers/deploy-containers/linux-containers)
