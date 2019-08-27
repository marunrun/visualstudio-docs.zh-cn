---
title: ASP.NET 调试：系统要求 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications, system requirements
- debugging ASP.NET Web applications, security requirements
ms.assetid: 7810b9b2-debf-4271-8fc7-1df031123255
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 63a94f9ae6c35ef304af334737a8f206da911afd
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402716"
---
# <a name="aspnet-debugging-system-requirements"></a>ASP.NET 调试：系统要求
本主题描述了 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 调试方案的软件和安全性要求：

- 本地调试：其中， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 和 Web 应用程序在同一台计算机上运行。 此方案有两种版本：

  - [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 代码驻留在文件系统中。

  - [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 代码驻留在 IIS 网站中。

- 远程调试：其中， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 在客户端计算机上运行，并对在远程服务器计算机上运行的 Web 应用程序进行调试。

## <a name="security-requirements"></a>安全性要求
 对于远程调试，本地和远程计算机必须位于域设置或工作组设置上。

 若要调试 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程（由应用程序池托管），则必须具有调试该进程的权限。 默认情况下，IIS 6.0 之前的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序作为“ASPNET”用户运行。 在 IIS 6.0 和 IIS 7.0 中，“网络服务”帐户为默认帐户。 如果工作进程作为“ASPNET”或“网络服务”运行，则必须具有管理员权限才能对其进行调试。

 > [!IMPORTANT]
 > 从 Windows Server 2008 R2 开始，我们建议使用[ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities)作为为每个应用程序池标识。

 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 辅助进程的名称根据调试方案和 IIS 版本的不同而不同。 有关详细信息，请参阅[如何：查找 ASP.NET 进程名称](../debugger/how-to-find-the-name-of-the-aspnet-process.md)。

 可以通过编辑运行 IIS 的服务器上的 machine.config 文件来更改运行 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程的用户帐户。 执行此操作的最佳方式是使用 Internet Information Services (IIS) 管理器。 有关详细信息，请参阅[如何：在用户帐户下运行工作进程](../debugger/how-to-run-the-worker-process-under-a-user-account.md)。

 如果将 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程更改为在自己的用户帐户下运行，则即使不是运行 IIS 的服务器上的管理员也可。

> [!CAUTION]
> 在将 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程更改为在其他帐户下运行之前，请考虑如果 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程在该帐户下运行时遭到黑客攻击可能会产生的后果。 “ASPNET”和“网络服务”用户帐户以最低的权限运行，减少了进程被黑客攻击时可能造成的损害。 如果必须将 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 工作进程更改为在具有更大权限的帐户下运行，则会增加受损的可能性。

## <a name="see-also"></a>请参阅

- [调试 ASP.NET 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
- [如何：在用户帐户下运行工作进程](../debugger/how-to-run-the-worker-process-under-a-user-account.md)