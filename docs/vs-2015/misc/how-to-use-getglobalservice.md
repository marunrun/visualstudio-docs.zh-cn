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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62948177"
---
# <a name="how-to-use-getglobalservice"></a>如何：使用 GetGlobalService
有时您可能需要从工具窗口中获得的服务或控制已没有已就位，否则使用并不了解所需的服务的服务提供商确定位置的容器。 例如，你可能想要写入活动日志从控件中。 有关这些及其他方案的详细信息，请参阅[如何：排查服务问题](../extensibility/how-to-troubleshoot-services.md)。  
  
 您可以充分[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]服务通过调用静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法。  
  
 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 依赖于任何 VSPackage 派生自第一次进行初始化的缓存的服务提供商<xref:Microsoft.VisualStudio.Shell.Package>确定位置。 必须保证，这种情况满足，否则为 null 的服务做好准备。  
  
 幸运的是，<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>大多数情况下正常工作。  
  
- 如果 VSPackage 提供的服务才知道另一个 VSPackage，VSPackage 请求该服务是就位之前提供此服务已加载的 VSPackage。  
  
- 如果 VSPackage 创建工具窗口，则 VSPackage 确定创建工具窗口之前位置。  
  
- 如果控件容器托管的 VSPackage 创建工具窗口，则 VSPackage 确定之前创建的控件容器位置。  
  
### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>若要获取从工具窗口或控件容器中的服务  
  
- 在构造函数、 工具窗口或控件容器中插入此代码：  
  
     [!code-csharp[UseGetGlobalService#1](../snippets/csharp/VS_Snippets_VSSDK/usegetglobalservice/cs/getglobalservicepackage.cs#1)]
     [!code-vb[UseGetGlobalService#1](../snippets/visualbasic/VS_Snippets_VSSDK/usegetglobalservice/vb/getglobalservicepackage.vb#1)]  
  
     此代码获取 SVsActivityLog 服务并将强制转换到<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口，可用于写入活动日志。 有关示例，请参见 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。  
  
## <a name="see-also"></a>请参阅  
 [如何：排查服务问题](../extensibility/how-to-troubleshoot-services.md)   
 [使用并提供服务](../extensibility/using-and-providing-services.md)   
 [服务基础知识](../extensibility/internals/service-essentials.md)