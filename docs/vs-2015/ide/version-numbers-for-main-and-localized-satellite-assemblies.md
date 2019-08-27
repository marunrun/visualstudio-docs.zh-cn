---
title: 主程序集和已本地化的附属程序集的版本号 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- satellite assemblies, version numbers
- SatelliteContractVersionAttribute
- version numbers, assemblies
- assemblies [Visual Studio], version numbers
- versioning, assemblies
ms.assetid: 5489aea1-57b4-4561-9bb4-24d490269602
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4e478f7da004aaffb892fd01532a35d813574d9a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696497"
---
# <a name="version-numbers-for-main-and-localized-satellite-assemblies"></a>用于主程序集和已本地化的附属程序集的版本号
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Resources.SatelliteContractVersionAttribute> 类为通过资源管理器使用本地化资源的主程序集提供版本控制支持。 通过将 <xref:System.Resources.SatelliteContractVersionAttribute> 应用于应用程序的主程序集，可在不更新其附属程序集的情况下，更新和重新部署该程序集。 例如，可以将 <xref:System.Resources.SatelliteContractVersionAttribute> 类与不会引入新资源的服务包配合使用，而无需重新生成和重新部署附属程序集。 若要使本地化资源可用，主程序集的附属协定版本必须与附属程序集的 <xref:System.Reflection.AssemblyVersionAttribute> 类匹配。 必须在 <xref:System.Resources.SatelliteContractVersionAttribute> 中指定确切的版本号；不允许使用通配符，如“*”。 有关详细信息，请参阅 [检索资源](https://msdn.microsoft.com/library/eca16922-1c46-4f68-aefe-e7a12283641f)。  
  
## <a name="updating-assemblies"></a>更新程序集  
 <xref:System.Resources.SatelliteContractVersionAttribute> 类允许在不更新附属程序集的情况下更新主程序集，反之亦然。 主程序集更新后，其程序集版本号也随之更新。 如果要继续使用现有附属程序集，请更改主程序集的版本号，但保持原有附属协定版本号。 例如，首次发布时，主程序集版本可能是 1.0.0.0。 附属程序集的附属协定版本和程序集版本也会是 1.0.0.0。 如果需要更新服务包的主程序集，可以将程序集版本更改为 1.0.0.1，同时将附属协定版本和附属程序集版本保持为 1.0.0.0。  
  
 如果需要更新附属程序集而不是主程序集，请更改附属程序集的 <xref:System.Reflection.AssemblyVersionAttribute>。 随附属程序集一起交付的还有策略程序集，该程序集说明新的附属程序集可与旧版附属程序集兼容。 有关策略的详细信息，请参阅[运行时如何定位程序集](https://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)。  
  
 下面的代码演示如何设置附属协定版本。 可以将代码放置在生成脚本或 AssemblyInfo.vb 或 AssemblyInfo.cs 文件中。  
  
```vb  
<Assembly: SatelliteContractVersionAttribute("4.3.2.1")>  
  
```  
  
```csharp  
[assembly: SatelliteContractVersionAttribute("4.3.2.1")]  
```  
  
## <a name="see-also"></a>请参阅  
 [运行时如何定位程序集](https://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)   
 [设置程序集属性](https://msdn.microsoft.com/library/36a98a81-b5b5-4c19-912a-11f91eff7f4e)   
 [安全性和已本地化的附属程序集](../ide/security-and-localized-satellite-assemblies.md)   
 [本地化应用程序](../ide/localizing-applications.md)   
 [对应用程序进行全球化和本地化](../ide/globalizing-and-localizing-applications.md)
