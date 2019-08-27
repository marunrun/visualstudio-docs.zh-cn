---
title: 在注册表中的 Windows 工具 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186387"
---
# <a name="tool-windows-in-the-registry"></a>注册表中的工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

提供的工具窗口的 Vspackage 必须使用注册[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]为工具窗口提供程序。 通过使用 Visual Studio 包模板创建的工具窗口默认情况下执行此操作。 工具窗口提供程序具有指定可见性属性，例如默认工具窗口大小和位置，用作工具窗口窗格和停靠样式的窗口的 GUID 的系统注册表项。  
  
 在开发期间，托管的工具窗口提供程序注册工具窗口，方法是： 将属性添加到源代码，然后在生成的程序集上运行 RegPkg.exe 实用程序。 有关详细信息，请参阅[注册工具窗口](../extensibility/registering-a-tool-window.md)。  
  
## <a name="registering-unmanaged-tool-window-providers"></a>注册非托管的工具窗口提供程序  
 非托管的工具窗口提供程序必须使用注册[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]ToolWindows 节的系统注册表。 下面的.reg 文件片断演示如何动态工具窗口可能在注册：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\<version number>\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}]  
@="{01069cdd-95ce-4620-ac21-ddff6c57f012}"  
"Name"="Microsoft.Samples.VisualStudio.IDE.ToolWindow.DynamicWindowPane"  
"Float"="250, 250, 410, 430"  
"DontForceCreate"=dword:00000001  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}\Visibility]  
"{f1536ef8-92ec-443c-9ed7-fdadf150da82}"=dword:00000000  
```  
  
 在上面的示例中的第一个项的版本编号是版本的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，如 7.1 或 8.0，子项 {f0e1e9a1-9860-484d-ad5d-367d79aabf55} 是工具窗口窗格 (DynamicWindowPane) 和默认值 {的 GUID01069cdd-95ce-4620-ac21-ddff6c57f012} 是 VSPackage 提供的工具窗口的 GUID。 浮点型和 DontForceCreate 的子项的说明，请参阅[工具窗口中显示配置](../extensibility/tool-window-display-configuration.md)。  
  
 第二个可选键 ToolWindows\Visibility，指定需要的工具窗口，要使其可见的命令的 Guid。 在这种情况下，没有指定的命令。 有关详细信息，请参阅[工具窗口中显示配置](../extensibility/tool-window-display-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [VSPackage 要点](../misc/vspackage-essentials.md)
