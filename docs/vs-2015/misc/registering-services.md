---
title: 注册服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- services, registering
ms.assetid: c4ebac40-0374-4dda-948e-06fdda0e9c81
caps.latest.revision: 8
manager: jillfra
ms.openlocfilehash: 64f2afa6e853978e919e466f91475bed1e8d698c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971285"
---
# <a name="registering-services"></a>注册服务
若要支持按需加载，服务提供商必须用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]注册其全球服务。  
  
 在开发期间，托管服务提供商通过将特性添加到包的源代码，然后在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE中生成包，从而注册服务和服务重写。 这会在生成的程序集上运行 RegPkg.exe 实用程序，注册包并为部署做准备。 有关详细信息，请参阅[如何：注册服务](../misc/how-to-register-a-service.md)。  
  
 非托管服务提供商必须用系统注册表中的服务节或服务重写节中的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 注册它们提供的服务。 下面的.reg 文件片断演示注册服务 SVsTextManager 的方式：  
  
```  
[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]  
@="{F5E7E720-1401-11d1-883B-0000F87579D2}"  
"Name"="SVsTextManager"  
```  
  
 在上面的示例中，版本号是版本 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]（如 7.1 或 8.0），注册表项 {F5E7E71D-1401-11d1-883B-0000F87579D2} 是 SVsTextManager 服务的服务标识符 (SID)，默认值 {F5E7E720-1401-11d1-883B-0000F87579D2} 是提供服务的文本管理器 VSPackage 的包 GUID。  
  
## <a name="remote-services-and-background-threads"></a>远程服务和后台线程  
 你提供的服务不会自动在远程方式下可用，或供后台线程使用。 若要使其可用，必须生成并注册类型库。  
  
 通过使用 Visual Studio 库 (VSL) 的非托管代码，可以通过这种方式注册类型库：  
  
```  
#define VSL_REGISTER_TYPE_LIB TRUE  
#include <VSLPackageDllEntryPoints.cpp>  
```  
  
 通过托管代码，可以添加如下生成后步骤：  
  
```  
regasm /tlb MyAssembly.dll  
```  
  
## <a name="see-also"></a>请参阅  
 [使用并提供服务](../extensibility/using-and-providing-services.md)   
 [服务基础知识](../extensibility/internals/service-essentials.md)