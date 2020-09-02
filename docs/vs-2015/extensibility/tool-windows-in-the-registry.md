---
title: 注册表中的工具窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering
ms.assetid: c4bb8add-7148-49e4-a377-01d059fd5524
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8cedb95ccd98c3d5bd5e05086cfd1b53b0f97cd9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186387"
---
# <a name="tool-windows-in-the-registry"></a>注册表中的工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

提供工具的 Vspackage 必须注册 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 为工具窗口提供程序。 默认情况下，使用 Visual Studio 包模板创建的工具窗口执行此操作。 工具窗口提供程序具有指定可见性属性的系统注册表项，如默认工具窗口大小和位置、用作工具窗口窗格的窗口的 GUID 和停靠样式。  
  
 在开发过程中，托管工具窗口提供程序通过将属性添加到源代码，然后在生成的程序集上运行 RegPkg.exe 实用程序来注册工具窗口。 有关详细信息，请参阅 [注册工具窗口](../extensibility/registering-a-tool-window.md)。  
  
## <a name="registering-unmanaged-tool-window-providers"></a>注册非托管工具窗口提供程序  
 非托管工具窗口提供程序必须 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 在系统注册表的 ToolWindows 部分中进行注册。 以下 .reg 文件片段显示动态工具窗口的注册方式：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\<version number>\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}]  
@="{01069cdd-95ce-4620-ac21-ddff6c57f012}"  
"Name"="Microsoft.Samples.VisualStudio.IDE.ToolWindow.DynamicWindowPane"  
"Float"="250, 250, 410, 430"  
"DontForceCreate"=dword:00000001  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}\Visibility]  
"{f1536ef8-92ec-443c-9ed7-fdadf150da82}"=dword:00000000  
```  
  
 在上面示例中的第一个键，版本号是的版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，例如7.1 或8.0，子项 {f0e1e9a1-9860-484d-ad5d-367d79aabf55} 是工具窗口窗格 (DynamicWindowPane) 的 guid，默认值 {01069cdd-4620 95ce-ac21-ddff6c57f012} 是提供工具窗口的 VSPackage 的 guid。 有关 Float 和 DontForceCreate 子项的说明，请参阅 [工具窗口显示配置](../extensibility/tool-window-display-configuration.md)。  
  
 第二个可选键 ToolWindows\Visibility 指定需要将工具窗口变为可见的命令的 Guid。 在这种情况下，未指定命令。 有关详细信息，请参阅 [工具窗口显示配置](../extensibility/tool-window-display-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [VSPackage 要点](../misc/vspackage-essentials.md)
