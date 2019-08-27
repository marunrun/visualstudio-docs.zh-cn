---
title: 状态持久性支持 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- state persistence, managed package framework support
- managed package framework, state persistence support
- state, persistence
ms.assetid: d25866f2-8d1f-477f-8aa5-3af3fbbf6e97
caps.latest.revision: 15
manager: jillfra
ms.openlocfilehash: 6dc542d2e410b79a21e436a1881c06bd3cc4eef8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62434314"
---
# <a name="support-for-state-persistence"></a>状态持久性支持
[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 可以维护公共对象的状态。 例如，解决方案和项目属性将保存到和从解决方案和项目文件中还原。 可以导出到和从设置文件导入用户设置。  
  
 Vspackage 通常依赖于本地存储区，在系统注册表中或在当前用户或计算机的应用程序数据文件夹中。 对于存储，如整数和字符串，需要少量的空间的值通常存储在系统注册表中。 对于存储，如位图，需要大量空间的值保存在文件中。 文件的路径可以本身保存在系统注册表中。 持久性机制必须有权访问本地存储。  
  
## <a name="support-for-locating-local-storage"></a>查找本地存储的支持  
 <xref:Microsoft.VisualStudio.Shell.Package>类提供支持在当前用户或计算机的系统注册表或应用程序数据文件夹中查找状态信息。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>  
 返回本地计算机的注册表根目录的路径[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，例如，HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0Exp。  
  
 从获取本地注册表根<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>服务。 如果这是不可用，会从获取<xref:Microsoft.VisualStudio.Shell.DefaultRegistryRootAttribute>VSPackage 的属性。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>  
 返回当前用户的 （每台计算机） 的路径的注册表根[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，例如，HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp。  
  
 从获取本地注册表根<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>服务。 如果这是不可用，则是由 VSPackage 的 DefaultLocalRegistryRoot 属性获得。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserDataPath%2A>  
 返回用作公共储存库的目录的路径[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]例如，C:\Documents and Settings 的当前漫游用户数据\\*YourAccountName*\applicationVisualStudio\8.0Exp。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserLocalDataPath%2A>  
 返回用作公共储存库的目录的路径[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的当前非漫游用户数据，例如，C:\Documents and Settings\\*YourAccountName*settings\applicationData\Microsoft\VisualStudio\8.0Exp。  
  
## <a name="see-also"></a>请参阅  
 [VSPackage 状态](../misc/vspackage-state.md)