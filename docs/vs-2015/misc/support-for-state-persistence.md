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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62434314"
---
# <a name="support-for-state-persistence"></a>状态持久性支持
[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 可以维护公共对象的状态。 例如，解决方案和项目属性保存到解决方案和项目文件，并从中还原。 用户设置可以导出到设置文件并从其导入。  
  
 Vspackage 通常依赖于本地存储，无论是在系统注册表中还是在当前用户或计算机的应用程序数据文件夹中。 对于存储需要少量空间（如整数和字符串）的值通常存储在系统注册表中。 需要大量存储空间（如位图）的值将保存在文件中。 文件路径本身可保存在系统注册表中。 持久性机制必须具有访问本地存储区的权限。  
  
## <a name="support-for-locating-local-storage"></a>支持查找本地存储  
 <xref:Microsoft.VisualStudio.Shell.Package>类提供对当前用户或计算机的系统注册表或应用程序数据文件夹中的状态信息的支持。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.ApplicationRegistryRoot%2A>  
 返回本地计算机的注册表根目录的路径 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，例如 HKEY_LOCAL_MACHINE \software\microsoft\visualstudio\8.0exp。  
  
 本地注册表根是从服务获取的 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> 。 如果这不可用，则从 <xref:Microsoft.VisualStudio.Shell.DefaultRegistryRootAttribute> VSPackage 的属性获取。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A>  
 返回 (每台计算机的当前用户的路径，) 注册表根目录 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，例如 HKEY_CURRENT_USER \software\microsoft\visualstudio\8.0exp。  
  
 本地注册表根是从服务获取的 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> 。 如果这不可用，则将从 VSPackage 的 DefaultLocalRegistryRoot 属性中获取。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserDataPath%2A>  
 返回作为当前漫游用户的数据的公共存储库的目录的路径 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，例如，c:\documents and 和 Settings \\ *YourAccountName*\Application Data\Microsoft\VisualStudio\8.0Exp。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.UserLocalDataPath%2A>  
 返回用作当前非漫游用户的数据的公共存储库的目录的路径 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，例如，c:\documents and 和 Settings \\ *YourAccountName*\Local Settings\Application Data\Microsoft\VisualStudio\8.0Exp。  
  
## <a name="see-also"></a>另请参阅  
 [VSPackage 状态](../misc/vspackage-state.md)