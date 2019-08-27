---
title: 部署概述 | Microsoft Docs
ms.custom: seodec18
ms.date: 06/22/2018
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
ms.openlocfilehash: b7c322b960360231c2e8a1d2aa1a9920bbcf5521
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263304"
---
# <a name="overview-of-deployment-in-visual-studio"></a>Visual Studio 中的部署概述

通过部署应用程序、服务或组件，你可以将其分发以便安装于其他计算机、设备、服务器或云中。 你需要在 Visual Studio 中为所需的部署类型选择适当的方法。

对于许多常见的应用类型，可在 Visual Studio 中直接从解决方案资源管理器部署应用程序。 有关此功能的快速概览，请参阅[初探部署](../deployment/deploying-applications-services-and-components.md)。

![选择发布选项](../deployment/media/quickstart-publish-azure.png)

## <a name="what-publishing-options-are-right-for-me"></a>哪些发布选项适合我？

在 Visual Studio 中，应用程序可以直接发布到以下目标：

- [Azure 应用服务](#azure-app-service)
- [Azure 虚拟机](#azure-virtual-machines)
- [文件系统](#file-system)
- [自定义目标（如 IIS、FTP 等）](#custom-targets-iis-ftp)，包括所有任意的 Web 服务器。

在“发布”选项卡上，可以选择现有发布配置文件、导入现有发布配置文件或使用此处所述的选项新建发布配置文件。 若要查看教程了解 IDE 中针对不同应用类型的发布选项，请参阅[初探部署](../deployment/deploying-applications-services-and-components.md)。

## <a name="azure-app-service"></a>Azure 应用服务

[Azure 应用服务](/azure/app-service/app-service-web-overview)和 [Linux 应用服务](/azure/app-service/containers/app-service-linux-intro)帮助开发人员快速创建各种可缩放的 Web 应用程序和服务，而无需维护基础结构。

用户可通过为包含的应用服务选择[定价层或计划](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)来确定应用服务具有的计算能力。 而且不必更改定价层就能让多个 Web 应用（和其他应用类型）共享同一个应用服务。 例如，可以在同一个应用服务上同时托管开发、过渡和生产 Web 应用。

应用服务在 Azure 的云托管虚拟机上运行，但这些虚拟机是为你而托管的。 应用服务中的每个应用均分配有一个唯一的 \*.azurewebsites.net URL；除免费层以外的所有定价层允许向站点分配自定义域名。

### <a name="when-to-choose-azure-app-service"></a>何时选用 Azure 应用服务

- 希望部署可通过 Internet 访问的 Web 应用程序。
- 希望根据需求自动缩放 Web 应用程序，而无需重新部署。
- 无需维护服务器基础结构（包括软件更新）。
- 不需要在托管 Web 应用程序的服务器上进行任何计算机级别的自定义设置。

> 如果想在自己的数据中心或其他本地计算机中使用 Azure 应用服务，可以使用 [Azure 堆栈](https://azure.microsoft.com/overview/azure-stack/)来实现。

有关发布到应用服务的详细信息，请参阅[快速入门 - 发布到 Azure 应用服务](quickstart-deploy-to-azure.md)和[快速入门 - 将 ASP.NET Core 发布到 Linux](quickstart-deploy-to-linux.md)。

## <a name="azure-virtual-machines"></a>Azure 虚拟机

[Azure 虚拟机 (VM)](https://azure.microsoft.com/documentation/services/virtual-machines/) 可用于在云中创建和管理任意数量的计算资源。 通过负责 VM 上的所有软件和更新，你可以根据应用程序的需求尽可能地对这些 VM 进行自定义。 此外，可以通过远程桌面直接访问虚拟机，只要需要，各服务器就会一直维持分配给它的 IP 地址。

缩放虚拟机上托管的应用程序时，需要根据需求起转额外的 VM，然后部署必要的软件。 利用这种额外的控制能力，可以在全球不同区域以不同方式进行缩放。 例如，如果应用程序要为多个地区办事处的员工提供服务，则可以根据这些地区的员工人数来缩放 VM，从而潜在地降低成本。

有关其他信息，请参阅 Azure 应用服务、Azure 虚拟机以及可通过 Visual Studio 中的“自定义”选项设置为部署目标的其他 Azure 服务之间的[详细比较](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/)。

### <a name="when-to-choose-azure-app-virtual-machines"></a>何时选用 Azure 应用虚拟机

- 希望部署可通过 Internet 访问的 Web 应用程序，并能完全控制所分配 IP 地址的生存期。
- 需要在服务器上进行计算机级别的自定义设置，其中包括诸如专用数据库系统、特定网络配置、磁盘分区之类的附加软件。
- 希望精细地控制 Web 应用程序的缩放。
- 出于任何其他原因，需要直接访问托管应用程序的服务器。

> 如果想在自己的数据中心或其他本地计算机中使用 Azure 虚拟机，可以使用 [Azure 堆栈](https://azure.microsoft.com/overview/azure-stack/)来实现。

## <a name="file-system"></a>文件系统

部署到文件系统意味着只需将应用程序文件复制到你自己的计算机上的特定文件夹中。 这种部署方式最常用于测试目的，如果计算机还运行服务器，则可以通过这种方式将应用程序部署为供数量有限的人员使用。 如果目标文件夹在网络上共享，那么，通过部署到文件系统能够使 Web 应用程序文件可供其他人访问，这些人随后可将其部署到特定服务器。

任何运行服务器的本地计算机都可以使应用程序能够通过 Internet 或 Intranet（取决于其配置方式和所连接的网络）访问。 （如果将计算机直接连接到 Internet，应特别小心，以免其受到外部安全威胁。）这些计算机由你管理，因此你可以完全控制软件和硬件配置。

请注意，如果出于任何原因（如计算机访问权限）不能使用云服务，例如 Azure 应用服务或 Azure 虚拟机，可以在自己的数据中心使用 [Azure 堆栈](https://azure.microsoft.com/overview/azure-stack/)。 Azure 堆栈可用于通过 Azure 应用服务和 Azure 虚拟机来管理并使用计算资源，并且让所有资源仍然保留在本地。

### <a name="when-to-choose-file-system-deployment"></a>何时选用文件系统部署

- 仅需要将应用程序部署到文件共享，其他人可从中将其部署到不同的服务器。
- 仅需要本地测试部署。
- 在将应用程序文件发送到另一个部署目标之前，想单独对文件进行检查并在必要时进行修改。

有关详细信息，请参阅[快速入门 - 部署到本地文件夹](quickstart-deploy-to-local-folder.md)

## <a name="custom-targets-iis-ftp"></a>自定义目标 (IIS、FTP)

利用自定义目标，可以将应用程序部署到 Azure 应用服务、Azure 虚拟机或本地文件系统以外的目标。 它可以部署到你有权访问的文件系统或任何其他服务器（Internet 或 Intranet），包括其他云服务上的服务器。 它可以与 Web 部署（文件或 .ZIP）和 FTP 配合使用。

如果选择自定义目标，Visual Studio 会提示输入配置文件名称，然后收集包括目标服务器或位置、站点名称和凭据在内的其他**连接**信息。 可以在“设置”选项卡上控制以下行为：

- 要部署的配置。
- 是否从目标中删除现有文件。
- 是否在发布期间预编译。
- 是否要从部署中排除 App_Data 文件夹中的文件。

可以在 Visual Studio 中创建任意数量的自定义部署配置文件，从而使得能够管理设置不同的配置文件。

### <a name="when-to-choose-custom-deployment"></a>何时选用自定义部署

- 在除 Azure 以外的可通过 URL 访问的提供程序上使用云服务。
- 希望用来进行部署的凭据不是在 Visual Studio 中所用的凭据或直接与 Azure 帐户相关联的凭据。
- 希望在每次部署时从目标中删除文件。

有关详细信息，请参阅[快速入门 - 部署到网站](quickstart-deploy-to-a-web-site.md)

## <a name="next-steps"></a>后续步骤

教程：

- [使用发布工具部署 .NET Core 应用程序](/dotnet/core/deploying/deploy-with-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [将 ASP.NET Core 应用发布到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [Visual C++ 中的部署](/cpp/windows/deployment-in-visual-cpp)
- [部署 UWP 应用](/windows/uwp/packaging/packaging-uwp-apps?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [使用 Web 部署将 Node.js 应用发布到 Azure](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
- [将 Python 应用发布到 Azure 应用服务](../python/publishing-python-web-applications-to-azure-from-visual-studio.md?toc=/visualstudio/deployment/toc.json&bc=/visualstudio/deployment/_breadcrumb/toc.json)
