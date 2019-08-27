---
title: 应用程序部署必备 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, platform detection
- ClickOnce deployment, prerequisites
- ClickOnce deployment, dependencies
- prerequisites, ClickOnce
- dependencies, ClickOnce
ms.assetid: fc6e047e-ad94-44e8-8ff5-b6d1f4ca7735
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8206e199acc3ccb76cf89603d48bed0173129218
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746061"
---
# <a name="application-deployment-prerequisites"></a>应用程序部署必备

若要成功安装和运行应用程序，首先安装应用程序所依赖到目标计算机上的所有组件。 例如，大多数应用程序创建使用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]具有.NET Framework 的依赖关系。 在这种情况下，公共语言运行时的正确版本必须存在于目标计算机上之前安装了应用程序。

 可以选择在这些系统必备组件**Prerequisites Dialog Box**和您的安装过程中安装.NET Framework 和任何其他可再发行组件。 此做法称为“引导”  。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成一个名为 Windows 可执行程序*Setup.exe*，也称为*引导程序*。 引导程序负责在运行应用程序之前，安装这些系统必备组件。 有关选择这些系统必备组件的详细信息，请参阅[系统必备组件对话框](../ide/reference/prerequisites-dialog-box.md)。

 每个系统必备组件都是一个引导程序包。 引导程序包是一组目录和文件，其中包含描述如何安装必备组件的清单文件。 如果应用程序的系统必备组件未列在“系统必备组件对话框”中，可以创建自定义引导程序包，将其添加到 Visual Studio  。 然后便可在“系统必备组件对话框”中选择这些系统必备组件  。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

 默认情况下，ClickOnce 部署可以使用引导。 对为 ClickOnce 部署生成的引导程序进行签名。 您可以禁用引导组件，但仅当您确信所有目标计算机上已安装正确版本的组件。

## <a name="bootstrapping-and-clickonce-deployment"></a>引导和 ClickOnce 部署
 在客户端计算机上安装应用程序之前[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]检查客户端，确保其中包含应用程序清单中指定的要求。 这些包括以下要求：

- 公共语言运行时的最低要求版本（在应用程序清单中被指定为一个程序集依赖项）。

- 应用程序要求的 Windows 操作系统的最低要求版本（在应用程序清单中使用 `<osVersionInfo>` 元素指定）。 (请参阅[\<依赖项 > 元素](../deployment/dependency-element-clickonce-application.md)。)

- 必须预先安装在全局程序集缓存 (GAC) 中，指定的程序集清单中的程序集依赖项声明的所有程序集的最小版本。

  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可以检测到缺少的先决条件，并可以使用引导程序来安装系统必备组件。 有关详细信息，请参阅[如何：将系统必备与 ClickOnce 应用程序一起安装](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)。

> [!NOTE]
> 若要更改由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 和 MageUI.exe 之类的工具生成的清单中的默认值，需要在文本编辑器中编辑应用程序清单，然后对应用程序清单和部署清单重新签名  。 有关详细信息，请参阅[如何：对应用程序清单和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

 如果你使用 Visual Studio 和 ClickOnce 来部署应用程序，则默认选中的引导程序包取决于解决方案中的 .NET Framework 版本。 但如果更改目标 .NET Framework 版本，则必须手动在“系统必备组件”对话框中更新选项  。

|目标 .NET Framework|选中的引导程序包|
|---------------------------|------------------------------------|
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows Installer 3.1|
|.NET Framework 4|.NET Framework 4<br /><br /> Windows Installer 3.1|

 通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布向导所生成的 Publish.htm 页指向仅安装应用程序的链接，或指向同时安装应用程序和引导组件的链接  。

 如果是使用 Visual Studio 中的 ClickOnce 发布向导或发布页生成的引导程序，则会自动为 Setup.exe 签名  。 但如果你希望使用客户的证书为引导程序签名，则可稍后对文件签名。

## <a name="bootstrapping-and-msbuild"></a>引导和 MSBuild
 如果不使用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，但而不是编译命令行上的应用程序，您可以创建[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]引导应用程序使用的 Microsoft Build Engine (MSBuild) 任务。 有关详细信息，请参阅[GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)。

 作为引导的替代方法，你可以使用电子软件分发系统（如 Microsoft Systems Management Server (SMS)）预先部署组件。

## <a name="bootstrapper-setupexe-command-line-arguments"></a>引导程序 (Setup.exe) 命令行参数
 *Setup.exe*生成的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]和 MSBuild 任务支持以下组命令行参数。 任何其他参数将转发到应用程序安装程序。

 如果更改了任何引导程序选项，必须更改未签名的引导程序，然后稍后登录引导程序文件。

| 命令行参数 | 描述 |
| - | - |
| **-h、-?、-Help** | 显示一个“帮助”对话框。 |
| **-url, -componentsurl** | 显示用于此安装的存储 URL 和组件 URL。 |
| **-url=** `location` | 设置 Setup.exe 将在其中查找 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的 URL  。 |
| **-componentsurl=** `location` | 设置 URL，其中*Setup.exe*将查找依赖项，如.NET Framework。 |
| **-homesite=** `true` **&#124;** `false` | 当`true`，从供应商的站点上的首选位置下载的依赖项。 此设置将替代 **-componentsurl**设置。 当`false`，从指定的 URL 下载的依赖项 **-componentsurl**。 |

## <a name="operating-system-support"></a>操作系统支持
 在 Windows Server 2008 Server Core 或 Windows Server 2008 R2 Server Core 上不支持 Visual Studio 引导程序，因为它们具有有限的功能提供低维护服务器环境。 例如，服务器核心安装选项仅支持.NET Framework 3.5 Server Core 配置文件，不能运行依赖于完整的.NET Framework 的 Visual Studio 功能。

## <a name="see-also"></a>请参阅
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)