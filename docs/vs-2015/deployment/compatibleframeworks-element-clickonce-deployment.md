---
title: '&lt;compatibleFrameworks&gt;元素 （ClickOnce 部署） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ef54062bd74c9395e187503dd12db1c0cd70d822
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65675419"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;compatibleFrameworks&gt;元素 （ClickOnce 部署）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识此应用程序可在其上安装和运行的 .NET Framework 版本。  
  
> [!NOTE]
> [MageUI.exe](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)不支持`compatibleFrameworks`元素时保存应用程序清单已签名证书使用[MageUI.exe](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)。 这种情况下必须使用 [Mage.exe](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)。  
  
## <a name="syntax"></a>语法  
  
```  
<compatibleFrameworks  
      SupportUrl>   
   <framework  
      targetVersion  
      profile  
      supportedRuntime  
   />   
</ compatibleFrameworks>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `compatibleFrameworks`元素是必需的部署清单面向[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]运行时提供的[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]或更高版本。 `compatibleFrameworks`元素包含一个或多个`framework`元素，用于指定此应用程序可以在其运行的.NET Framework 版本。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]运行时将运行该应用程序在第一个可用`framework`此列表中。  
  
 下表列出了该属性的`compatibleFrameworks`元素支持。  
  
|特性|描述|  
|---------------|-----------------|  
|`S` `upportUrl`|可选。 指定首选的兼容.NET Framework 版本，可以下载的 URL。|  
  
## <a name="framework"></a>框架  
 必需。 下表列出了属性的`framework`元素支持。  
  
|特性|描述|  
|---------------|-----------------|  
|`targetVersion`|必需。 指定的目标.NET Framework 的版本号。|  
|`profile`|必需。 指定目标.NET Framework 的配置文件。|  
|`supportedRuntime`|必需。 指定的目标.NET Framework 与相关联的运行时的版本号。|  
  
## <a name="remarks"></a>备注  
  
## <a name="example"></a>示例  
 下面的代码示例演示`compatibleFrameworks`中的元素[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署清单。 可以在上运行此部署[!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)]。 它还可以运行[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]因为它是一个超集[!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)]。  
  
```  
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">  
  <framework   
      targetVersion="4.0"   
      profile="Client"   
      supportedRuntime="4.0.30319" />  
</compatibleFrameworks>  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
