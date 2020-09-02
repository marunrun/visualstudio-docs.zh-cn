---
title: 如何：使用 GetGlobalService |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- services, GetGlobalService
ms.assetid: 4cdf5ab5-9f09-4caf-9011-2dcb2c62f1b7
caps.latest.revision: 14
manager: jillfra
ms.openlocfilehash: 1c1fb48e4bb354ef403b39b0f1320ead92f43967
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62948177"
---
# <a name="how-to-use-getglobalservice"></a>如何：使用 GetGlobalService
有时，可能需要从工具窗口或控件容器获取未被放置的服务，否则，可能会将其放置在不知道所需服务的服务提供程序中。 例如，你可能想要从控件内写入活动日志。 有关这些方案和其他方案的详细信息，请参阅 [如何：对服务进行故障排除](../extensibility/how-to-troubleshoot-services.md)。  
  
 可以 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 通过调用静态方法获取大多数服务 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 依赖于第一次从派生的任何 VSPackage 时初始化的缓存服务提供程序 <xref:Microsoft.VisualStudio.Shell.Package> 。 必须保证满足此条件，否则应为 null 服务做好准备。  
  
 幸运的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 是，大多数时间都能正常工作。  
  
- 如果 VSPackage 提供的服务只知道另一个 VSPackage，则请求该服务的 VSPackage 将在加载该服务的 VSPackage 之前放置。  
  
- 如果工具窗口是通过 VSPackage 创建的，则在创建工具窗口之前，VSPackage 被放置。  
  
- 如果控件容器由 VSPackage 所创建的工具窗口承载，则在创建控件容器之前，VSPackage 被放置。  
  
### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>从工具窗口或控件容器中获取服务  
  
- 在构造函数、工具窗口或控件容器中插入以下代码：  
  
     [!code-csharp[UseGetGlobalService#1](../snippets/csharp/VS_Snippets_VSSDK/usegetglobalservice/cs/getglobalservicepackage.cs#1)]
     [!code-vb[UseGetGlobalService#1](../snippets/visualbasic/VS_Snippets_VSSDK/usegetglobalservice/vb/getglobalservicepackage.vb#1)]  
  
     此代码获取 SVsActivityLog 服务并将其强制转换为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> 接口，该接口可用于写入活动日志。 有关示例，请参阅 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何：排除服务故障](../extensibility/how-to-troubleshoot-services.md)   
 [使用和提供服务](../extensibility/using-and-providing-services.md)   
 [服务基础知识](../extensibility/internals/service-essentials.md)