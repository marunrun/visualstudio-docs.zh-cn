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
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66745608"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>ClickOnce 部署中的安全、版本控制和清单问题

有多种问题[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]安全性、 应用程序版本控制和清单的语法和语义可能会导致[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署未成功完成。

## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce 和 Windows Vista 用户帐户控制

在[!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)]，默认情况下的应用程序作为标准用户运行，即使当前用户使用具有管理员权限的帐户登录。 如果应用程序必须执行需要管理员权限的操作，它告诉操作系统，然后会提示用户输入其管理员凭据。 此功能，为用户帐户控制 (UAC)，防止进行更改可能影响整个操作系统，而无需用户的明确批准的应用程序。 Windows 应用程序声明它们通过指定需要此权限提升`requestedExecutionLevel`属性中`trustInfo`其应用程序清单部分。

由于公开应用程序受到安全提升攻击的风险[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]如果客户端启用了 UAC，应用程序不能请求权限提升。 任何[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]尝试设置应用程序，其`requestedExecutionLevel`归于`requireAdministrator`或`highestAvailable`不会安装在[!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)]。

在某些情况下，你[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序可能会尝试使用管理员权限运行安装程序检测逻辑由于[!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)]。 在这种情况下，可以设置`requestedExecutionLevel`到应用程序清单中的特性`asInvoker`。 这会导致应用程序本身不用提升权限运行。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 自动将此特性添加到所有应用程序清单。

如果你正在开发的应用程序的整个生存期内需要管理员权限的应用程序，则应考虑部署应用程序改为使用 Windows Installer (MSI) 技术。 有关详细信息，请参阅[Windows Installer 基本知识](../extensibility/internals/windows-installer-basics.md)。

## <a name="online-application-quotas-and-partial-trust-applications"></a>联机应用程序的配额和部分信任应用程序

如果你[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]联机而不是通过安装应用程序运行，它必须在范围内保留设置为联机应用程序的配额。 此外，使用一组受限的安全权限，例如运行在部分信任环境中的网络应用程序不能大于配额大小的一半。

有关详细信息和有关如何更改联机应用程序配额的说明，请参阅[ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。

## <a name="versioning-issues"></a>版本问题

如果将强名称分配给您的程序集并递增程序集的版本号以反映应用程序更新，可能会遇到问题。 使用强名称的程序集的引用编译的任何程序集必须自行重新编译，或该程序集将尝试引用较旧版本。 程序集将尝试此操作由于程序集在其绑定请求中使用旧的版本值。

例如，假设在其自己的版本号为 1.0.0.0 的项目中有强名称的程序集。 在编译该程序集之后, 您将其添加为对包含主应用程序的项目的引用。 如果你更新该程序集、 递增的版本为 1.0.0.1，并尝试进行部署而无需重新编译应用程序，该应用程序不能在运行时将程序集加载。

正在编辑的情况下，才会出现此错误在[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]清单手动; 如果生成你的部署使用 Visual Studio，则不应遇到此错误。

## <a name="specify-individual-net-framework-assemblies-in-the-manifest"></a>在清单中指定单独的.NET Framework 程序集

你的应用程序将无法加载如果您已手动编辑[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署，以引用较旧版本的.NET Framework 程序集。 例如，如果添加到清单中指定的版本之前的.NET Framework 的版本的 System.Net 程序集的引用时，会发生错误。 一般情况下，您不应尝试指定单独的.NET Framework 程序集的引用如对其运行应用程序的.NET framework 的版本指定为应用程序清单中的依赖项。

## <a name="manifest-parsing-issues"></a>清单分析问题

通过使用清单文件[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]是 XML 文件，并且它们必须是格式正确且有效： 必须遵循 XML 语法规则，并且只能使用元素和相关的 XML 架构中定义的属性。

某些内容可能会导致问题，在清单文件中选择包含特殊字符，如单引号或双引号引起来标记应用程序的名称。 应用程序的名称是一部分其[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]标识。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 当前不会分析包含特殊字符的标识。 如果无法激活你的应用程序，请确保您使用仅按字母和数字字符的名称，并尝试重新部署它。

如果您已手动编辑部署或应用程序清单，您可能会无意中损坏它们。 清单损坏会阻止的正确[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]安装。 可以通过单击来在运行时调试此类错误**详细信息**上**ClickOnce 错误**对话框中，并读取日志中的错误消息。 日志将列出以下消息之一：

- 语法错误的行号和字符的描述发生错误的位置。

- 元素或属性在违反该清单的架构中使用的名称。 如果你已手动添加 XML，到对清单，必须将比较你添加到清单架构。 有关详细信息，请参阅[ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)并[ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)。

- ID 冲突。 部署和应用程序清单中的依赖关系引用必须是唯一在这种他们`name`和`publicKeyToken`属性。 如果在清单中任意两个元素之间的这两个属性匹配，清单分析将会失败。

## <a name="precautions-when-manually-changing-manifests-or-applications"></a>手动更改清单或应用程序时的注意事项

更新应用程序清单时，必须重新签名的应用程序清单和部署清单。 部署清单包含对包含该文件的哈希和其数字签名的应用程序清单的引用。

### <a name="precautions-with-deployment-provider-usage"></a>使用部署提供程序的注意事项

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署清单包含`deploymentProvider`属性用于从应安装并提供服务应用程序指向该位置的完整路径：

```xml
<deploymentProvider codebase="http://myserver/myapp.application" />
```

当设置此路径[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]创建应用程序，并为已安装应用程序。 路径指向的标准位置其中[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]安装程序将安装的应用程序和搜索更新。 如果您使用**xcopy**命令将复制[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序到另一个位置，但不能更改`deploymentProvider`属性，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]仍将引用返回到原始位置时它会尝试下载应用程序。

如果你想要移动或复制应用程序，则还必须更新`deploymentProvider`路径，以便在客户端实际安装从新位置。 正在更新此路径是主要是一个问题，如果你已安装应用程序。 联机应用程序通过设置的原始 URL 始终启动`deploymentProvider`是可选的。 如果`deploymentProvider`，则将起作用，否则，用于启动应用程序的 URL 将使用用作基 URL，以下载应用程序文件。

> [!NOTE]
> 每次更新的清单时您必须还对其签名再次。

## <a name="see-also"></a>请参阅

[ClickOnce 部署进行故障排除](../deployment/troubleshooting-clickonce-deployments.md)
[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
