---
title: ClickOnce 部署中的安全/版本控制/清单问题
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- versioning, ClickOnce applications
- ClickOnce applications, Windows Vista User Account Control
- ClickOnce applications, versioning issues
- security, ClickOnce applications
- Windows 7, ClickOnce deployments
- ClickOnce applications, manifest issues
- User Account Control, ClickOnce applications
- Windows Vista, ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, security issues
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb2ec5229132265feb1095c9ee921d73a1568dd2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66745608"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>ClickOnce 部署中的安全、版本控制和清单问题

存在许多有关 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安全、应用程序版本控制和清单语法和语义的问题，导致 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署不会成功。

## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce 和 Windows Vista 用户帐户控制

在中 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] ，默认情况下，应用程序作为标准用户运行，即使当前用户是使用具有管理员权限的帐户登录的。 如果应用程序必须执行需要管理员权限的操作，它会告知操作系统，然后系统会提示用户输入其管理员凭据。 此功能称为用户帐户控制 (UAC) ，可防止应用程序进行更改，这些更改可能会影响整个操作系统，而无需用户进行明确批准。 Windows 应用程序通过 `requestedExecutionLevel` 在应用程序清单的部分中指定特性来声明它们需要此权限提升 `trustInfo` 。

由于向安全提升攻击公开应用程序的风险， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 如果对客户端启用了 UAC，应用程序将无法请求权限提升。 任何 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 尝试将其属性设置为或的应用程序 `requestedExecutionLevel` `requireAdministrator` `highestAvailable` 将不会在上安装 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 。

在某些情况下， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可能会尝试以管理员权限运行，因为上安装程序检测逻辑 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 。 在这种情况下，你可以将 `requestedExecutionLevel` 应用程序清单中的特性设置为 `asInvoker` 。 这将导致应用程序本身无需提升便可运行。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 自动将此属性添加到所有应用程序清单。

如果正在开发的应用程序需要在应用程序的整个生存期内拥有管理员权限，则应考虑使用 Windows Installer (MSI) 技术来部署应用程序。 有关详细信息，请参阅 [Windows Installer 基础知识](../extensibility/internals/windows-installer-basics.md)。

## <a name="online-application-quotas-and-partial-trust-applications"></a>联机应用程序配额和部分信任应用程序

如果你 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的应用程序在联机时（而不是通过安装）运行，则必须将其放在为联机应用程序留出的配额内。 此外，在部分信任环境下运行的网络应用程序（如使用一组受限的安全权限）不能大于配额大小的一半。

有关详细信息以及如何更改联机应用程序配额的说明，请参阅 [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。

## <a name="versioning-issues"></a>版本问题

如果将强名称分配给程序集并递增程序集版本号以反映应用程序更新，则可能会遇到问题。 使用具有强名称的程序集的引用编译的任何程序集都必须重新编译，否则程序集将尝试引用较旧的版本。 由于程序集在其绑定请求中使用旧版本值，因此程序集将尝试这种情况。

例如，假设在其自己的项目中有一个版本为1.0.0.0 的强名称程序集。 编译程序集之后，将其添加为对包含主应用程序的项目的引用。 如果更新程序集，将版本递增为1.0.0.1，并尝试在不重新编译应用程序的情况下部署该程序集，则该应用程序将不能在运行时加载该程序集。

仅当手动编辑清单时才会发生此错误 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ; 如果使用 Visual Studio 生成部署，则不会遇到此错误。

## <a name="specify-individual-net-framework-assemblies-in-the-manifest"></a>指定清单中的单个 .NET Framework 程序集

如果已手动编辑某个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署以引用 .NET Framework 程序集的较早版本，则应用程序将无法加载。 例如，如果在清单中指定的版本之前添加了对 System.Net .NET Framework 程序集的引用，则会发生错误。 通常，您不应尝试指定对单个 .NET Framework 程序集的引用，因为您的应用程序运行时所在 .NET Framework 的版本在应用程序清单中指定为依赖项。

## <a name="manifest-parsing-issues"></a>清单分析问题

使用的清单文件 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 是 XML 文件，它们必须格式正确且有效：它们必须遵循 xml 语法规则并仅使用相关 xml 架构中定义的元素和属性。

在清单文件中可能会导致问题的原因是为应用程序选择的名称包含特殊字符，如单引号或双引号。 应用程序的名称是其标识的一部分 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 当前不分析包含特殊字符的标识。 如果你的应用程序无法激活，请确保该名称只使用字母和数字字符，然后再次尝试部署。

如果你已手动编辑了你的部署清单或应用程序清单，可能会无意中损坏它们。 损坏的清单将阻止正确的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装。 可以通过单击 " **ClickOnce 错误**" 对话框中的 "**详细信息**"，然后在日志中读取错误消息，在运行时调试此类错误。 日志将列出以下消息之一：

- 语法错误的说明，以及发生错误的行号和字符位置。

- 用于违反清单架构的元素或属性的名称。 如果已手动将 XML 添加到清单，则必须将添加内容与清单架构进行比较。 有关详细信息，请参阅 [clickonce 部署清单](../deployment/clickonce-deployment-manifest.md) 和 [clickonce 应用程序清单](../deployment/clickonce-application-manifest.md)。

- ID 冲突。 部署和应用程序清单中的依赖关系引用必须在其和属性中都是唯一的 `name` `publicKeyToken` 。 如果清单中的两个元素之间的两个属性匹配，则清单分析将不会成功。

## <a name="precautions-when-manually-changing-manifests-or-applications"></a>手动更改清单或应用程序时的注意事项

更新应用程序清单时，必须对应用程序清单和部署清单进行重新签名。 部署清单包含对应用程序清单的引用，该清单包含该文件的哈希值和数字签名。

### <a name="precautions-with-deployment-provider-usage"></a>部署提供程序使用注意事项

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署清单具有一个 `deploymentProvider` 属性，该属性指向从其安装和维护应用程序的位置的完整路径：

```xml
<deploymentProvider codebase="http://myserver/myapp.application" />
```

此路径是在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 创建应用程序时设置的，对安装的应用程序是强制的。 路径指向安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 程序将在其中安装应用程序的标准位置，并搜索更新。 如果使用 **xcopy** 命令将 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序复制到其他位置，但不更改 `deploymentProvider` 属性，则 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 在尝试下载应用程序时仍将引用原始位置。

如果要移动或复制应用程序，则还必须更新 `deploymentProvider` 路径，以便客户端从新位置实际安装。 如果你安装了应用程序，则更新此路径主要是个问题。 对于始终通过原始 URL 启动的联机应用程序，设置 `deploymentProvider` 是可选的。 如果 `deploymentProvider` 设置了，则将遵守此设置; 否则，用于启动应用程序的 url 将用作下载应用程序文件的基本 url。

> [!NOTE]
> 每次更新清单时，还必须对其进行重新签名。

## <a name="see-also"></a>另请参阅

[ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md) 
[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md) 
[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
