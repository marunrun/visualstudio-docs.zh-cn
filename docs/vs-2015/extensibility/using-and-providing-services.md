---
title: 使用并提供服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
caps.latest.revision: 42
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7f58e29797e9a7760aa0f48c68868199f51b3c92
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68177431"
---
# <a name="using-and-providing-services"></a>使用并提供服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

服务是两个 Vspackage 之间的协定。 一个 VSPackage 提供了一组特定的另一个 VSPackage 来使用的接口。 例如，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]提供了<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>服务到任何 VSPackage 它加载。 此服务提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口，可用于写入活动日志。 有关更多信息，请参见[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。  
  
 Vspackage 可以提供其自己的使用的服务<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>接口...  
  
 Visual Studio 提供了重要的服务，如下所示：  
  
|IDE 服务|描述|  
|-----------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|提供了访问 IDE 的基本功能、 Vspackage、 与注册表服务处理。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供了基本窗口化和在 IDE 中，如创建工具和文档窗口的功能与 UI 相关的功能。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供了基本解决方案相关的功能，例如用于枚举项目、 创建新项目，以及监视项目的更改的功能。|  
  
## <a name="in-this-section"></a>本节内容  
 [服务基础知识](../extensibility/internals/service-essentials.md)  
 提供了 Visual Studio 服务的重要元素。  
  
 [如何：获取服务](../extensibility/how-to-get-a-service.md)  
 介绍如何请求 （使用） 服务。  
  
 [如何：提供服务](../extensibility/how-to-provide-a-service.md)  
 讨论如何提供服务。  
  
 [如何：提供异步 Visual Studio 服务](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)  
 讨论如何提供异步服务。  
  
 [如何：进行服务的故障排除](../extensibility/how-to-troubleshoot-services.md)  
 讨论常见的问题并提供了这些解决方案。  
  
## <a name="related-sections"></a>相关章节  
 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)
