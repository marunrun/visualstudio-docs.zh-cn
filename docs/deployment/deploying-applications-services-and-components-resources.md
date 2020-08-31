---
title: 将 Visual Studio 应用部署到文件夹、IIS、Azure 或其他目标
description: 详细了解如何使用发布向导发布应用的选项
ms.custom: contperfq1
ms.date: 08/21/2020
ms.topic: overview
dev_langs:
- FSharp
- VB
- CSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7125be46a894072f034bf1fce3060d2bda564aff
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88800823"
---
# <a name="deploy-your-app-to-a-folder-iis-azure-or-another-destination"></a>将应用部署到文件夹、IIS、Azure 或其他目标

通过部署应用程序、服务或组件，你可以将其分发以便安装于其他计算机、设备、服务器或云中。 你需要在 Visual Studio 中为所需的部署类型选择适当的方法。

对于许多常见的应用类型，可在 Visual Studio 中直接从解决方案资源管理器部署应用程序。 有关此功能的快速概览，请参阅[初探部署](../deployment/deploying-applications-services-and-components.md)。

![选择发布选项](../deployment/media/quickstart-publish-dialog.png)

## <a name="what-publishing-options-are-right-for-me"></a>哪些发布选项适合我？

在 Visual Studio 中，应用程序可以直接发布到以下目标：

- [Azure](#azure)
- [Docker 容器注册表](#docker-container-registry)
- [文件夹](#folder)
- [FTP/FTPS 服务器](#ftpftps-server)
- [Web 服务器 (IIS)](#web-server-iis)
- [导入配置文件](#import-profile)

## <a name="azure"></a>Azure 

当你选择 Azure 时，可以在以下选项中进行选择：

- 在 Windows、Linux 上运行或作为 Docker 映像运行的 Azure 应用服务
- 部署到 Azure 容器注册表的 Docker 映像
- Azure 虚拟机

![选择一项 Azure 服务](../deployment/media/quickstart-choose-azure-service.png)

### <a name="azure-app-service"></a>Azure 应用服务

[Azure 应用服务](/azure/app-service/app-service-web-overview)帮助开发人员快速创建可缩放的 Web 应用程序和服务，而无需维护基础结构。 应用服务在 Azure 的云托管虚拟机上运行，但这些虚拟机是为你而托管的。 应用服务中的每个应用均分配有一个唯一的 \*.azurewebsites.net URL；除免费层以外的所有定价层允许向站点分配自定义域名。

用户可通过为包含的应用服务选择[定价层或计划](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)来确定应用服务具有的计算能力。 而且不必更改定价层就能让多个 Web 应用（和其他应用类型）共享同一个应用服务。 例如，可以在同一个应用服务上同时托管开发、过渡和生产 Web 应用。

#### <a name="when-to-choose-azure-app-service"></a>何时选用 Azure 应用服务

- 希望部署可通过 Internet 访问的 Web 应用程序。
- 希望根据需求自动缩放 Web 应用程序，而无需重新部署。
- 无需维护服务器基础结构（包括软件更新）。
- 不需要在托管 Web 应用程序的服务器上进行任何计算机级别的自定义设置。

> 如果想在自己的数据中心或其他本地计算机中使用 Azure 应用服务，可以使用 [Azure 堆栈](https://azure.microsoft.com/overview/azure-stack/)来实现。

有关发布到应用服务的详细信息，请参阅以下链接：
- [快速入门 - 发布到 Azure 应用服务](quickstart-deploy-to-azure.md)和[快速入门 - 将 ASP.NET Core 发布到 Linux](quickstart-deploy-to-linux.md)。
- [对 Azure 应用服务和 IIS 上的 ASP.NET Core 进行故障排除](/aspnet/core/test/troubleshoot-azure-iis)。

### <a name="azure-container-registry"></a>Azure 容器注册表

使用 [Azure 容器注册表](/azure/container-registry/)，可以在专用注册表中为所有类型的容器部署生成、存储和管理 Docker 容器映像与项目。

#### <a name="when-to-choose-azure-container-registry"></a>何时选择 Azure 容器注册表

- 有现成的 Docker 容器开发和部署管道。
- 要在 Azure 中生成 Docker 容器映像。

### <a name="azure-virtual-machines"></a>Azure 虚拟机

[Azure 虚拟机 (VM)](https://azure.microsoft.com/documentation/services/virtual-machines/) 可用于在云中创建和管理任意数量的计算资源。 通过负责 VM 上的所有软件和更新，你可以根据应用程序的需求尽可能地对这些 VM 进行自定义。 此外，可以通过远程桌面直接访问虚拟机，只要需要，各服务器就会一直维持分配给它的 IP 地址。

缩放虚拟机上托管的应用程序时，需要根据需求起转额外的 VM，然后部署必要的软件。 利用这种额外的控制能力，可以在全球不同区域以不同方式进行缩放。 例如，如果应用程序要为多个地区办事处的员工提供服务，则可以根据这些地区的员工人数来缩放 VM，从而潜在地降低成本。

有关其他信息，请参阅 Azure 应用服务、Azure 虚拟机以及可通过 Visual Studio 中的“自定义”选项设置为部署目标的其他 Azure 服务之间的[详细比较](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/)。

#### <a name="when-to-choose-azure-virtual-machines"></a>何时选择 Azure 虚拟机

- 希望部署可通过 Internet 访问的 Web 应用程序，并能完全控制所分配 IP 地址的生存期。
- 需要在服务器上进行计算机级别的自定义设置，其中包括诸如专用数据库系统、特定网络配置、磁盘分区之类的附加软件。
- 希望精细地控制 Web 应用程序的缩放。
- 出于任何其他原因，需要直接访问托管应用程序的服务器。

> 如果想在自己的数据中心或其他本地计算机中使用 Azure 虚拟机，可以使用 [Azure 堆栈](https://azure.microsoft.com/overview/azure-stack/)来实现。

## <a name="docker-container-registry"></a>Docker 容器注册表

如果你的应用程序使用 Docker，则可以将容器化应用程序发布到 Docker 容器注册表。

### <a name="when-to-choose-docker-container-registry"></a>何时选择 Docker 容器注册表

- 需要部署容器化应用程序

## <a name="folder"></a>文件夹

部署到文件系统意味着只需将应用程序文件复制到你自己的计算机上的特定文件夹中。 这种部署方式最常用于测试目的，如果计算机还运行服务器，则可以通过这种方式将应用程序部署为供数量有限的人员使用。 如果目标文件夹在网络上共享，那么，通过部署到文件系统能够使 Web 应用程序文件可供其他人访问，这些人随后可将其部署到特定服务器。

任何运行服务器的本地计算机都可以使应用程序能够通过 Internet 或 Intranet（取决于其配置方式和所连接的网络）访问。 （如果将计算机直接连接到 Internet，应特别小心，以免其受到外部安全威胁。）这些计算机由你管理，因此你可以完全控制软件和硬件配置。

请注意，如果出于任何原因（如计算机访问权限）不能使用云服务，例如 Azure 应用服务或 Azure 虚拟机，可以在自己的数据中心使用 [Azure 堆栈](https://azure.microsoft.com/overview/azure-stack/)。 Azure 堆栈可用于通过 Azure 应用服务和 Azure 虚拟机来管理并使用计算资源，并且让所有资源仍然保留在本地。

### <a name="when-to-choose-file-system-deployment"></a>何时选用文件系统部署

- 仅需要将应用程序部署到文件共享，其他人可从中将其部署到不同的服务器。
- 仅需要本地测试部署。
- 在将应用程序文件发送到另一个部署目标之前，想单独对文件进行检查并在必要时进行修改。

有关详细信息，请参阅[快速入门 - 部署到本地文件夹](quickstart-deploy-to-local-folder.md)

## <a name="ftpftps-server"></a>FTP/FTPS 服务器

使用 FTP/FTPS 服务器可以将应用程序部署到 Azure 以外的服务器。 它可以部署到你有权访问的文件系统或任何其他服务器（Internet 或 Intranet），包括其他云服务上的服务器。 它可以与 Web 部署（文件或 .ZIP）和 FTP 配合使用。

如果选择 FTP/FTPS 服务器，Visual Studio 会提示输入配置文件名称，然后收集包括目标服务器或位置、站点名称和凭据在内的其他连接信息。 可以在“设置”选项卡上控制以下行为：

- 要部署的配置。
- 是否从目标中删除现有文件。
- 是否在发布期间预编译。
- 是否要从部署中排除 App_Data 文件夹中的文件。

可以在 Visual Studio 中创建任意数量的 FTP/FTPS 部署配置文件，从而管理设置不同的配置文件。

### <a name="when-to-choose-ftpftps-server-deployment"></a>何时选择 FTP/FTPS 服务器部署

- 在除 Azure 以外的可通过 URL 访问的提供程序上使用云服务。
- 希望用来进行部署的凭据不是在 Visual Studio 中所用的凭据或直接与 Azure 帐户相关联的凭据。
- 希望在每次部署时从目标中删除文件。

## <a name="web-server-iis"></a>Web 服务器 (IIS)

使用 IIS Web 服务器可以将应用程序部署到 Azure 以外的其他 Web 服务器。 它可以部署到你有权访问的 IIS 服务器（Internet 或 Intranet），包括其他云服务上的服务器。 它可以与 Web 部署或 Web 部署包一起使用。

如果选择 IIS Web 服务器，Visual Studio 会提示输入配置文件名称，然后收集包括目标服务器或位置、站点名称和凭据在内的其他连接信息。 可以在“设置”选项卡上控制以下行为：

- 要部署的配置。
- 是否从目标中删除现有文件。
- 是否在发布期间预编译。
- 是否要从部署中排除 App_Data 文件夹中的文件。

可以在 Visual Studio 中创建任意数量的 IIS Web 服务器部署配置文件，从而管理设置不同的配置文件。

### <a name="when-to-choose-web-server-iis-deployment"></a>何时选择 Web 服务器 (IIS) 部署

- 要使用 IIS 发布可通过 URL 访问的站点或服务。
- 希望用来进行部署的凭据不是在 Visual Studio 中所用的凭据或直接与 Azure 帐户相关联的凭据。
- 希望在每次部署时从目标中删除文件。

有关详细信息，请参阅[快速入门 - 部署到网站](quickstart-deploy-to-a-web-site.md)。 有关排查 IIS 上的 ASP.NET Core 故障的帮助信息，请参阅[排查 Azure 应用服务和 IIS 上的 ASP.NET Core 故障](/aspnet/core/test/troubleshoot-azure-iis)。

## <a name="import-profile"></a>导入配置文件

在发布到 IIS 或 Azure 应用服务时，可以导入配置文件。 可以使用发布设置文件 (\*.publishsettings)  配置部署。 发布设置文件由 IIS 或 Azure 应用服务创建，或者可手动创建，然后可将其导入 Visual Studio。

使用发布设置文件可以简化部署配置，与手动配置每个部署配置文件相比，在团队环境中效果更好。

### <a name="when-to-choose-import-profile"></a>何时选择导入配置文件

- 要发布到 IIS 并且要简化部署配置时。
- 要发布到 IIS 或 Azure 应用服务，并且需要加快部署配置速度，以便重用或让团队成员发布到同一服务时。

有关详细信息，请参阅以下主题：

- [导入发布设置并部署到 IIS](tutorial-import-publish-settings-iis.md)
- [导入发布设置并部署到 Azure](tutorial-import-publish-settings-azure.md)

## <a name="next-steps"></a>后续步骤

教程：

- [使用发布工具部署 .NET Core 应用程序](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [将 ASP.NET Core 应用发布到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Visual C++ 中的部署](/cpp/windows/deployment-in-visual-cpp)
- [部署 UWP 应用](/windows/uwp/packaging/packaging-uwp-apps?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [使用 Web 部署将 Node.js 应用发布到 Azure](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [将 Python 应用发布到 Azure 应用服务](../python/publishing-python-web-applications-to-azure-from-visual-studio.md?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
