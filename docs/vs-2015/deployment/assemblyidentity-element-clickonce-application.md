---
title: '&lt;assemblyIdentity&gt;元素 （ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce application manifest]
ms.assetid: f48e9531-efac-4d11-8166-f63a5ece1ac5
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5bde22809af69071f5484e25717a5aea7d78a603
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62428529"
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;assemblyIdentity&gt;元素 （ClickOnce 应用程序）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识应用程序部署在[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署。  
  
## <a name="syntax"></a>语法  
  
```  
  
      <assemblyIdentity   
   name  
   version  
   publicKeyToken  
   processorArchitecture  
   language  
/>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `assemblyIdentity`元素是必需的。 它不包含任何子元素，并具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Name`|必需。 标识应用程序的名称。<br /><br /> 如果`Name`包含特殊字符，如单引号或双引号引起来，应用程序可能无法激活。|  
|`Version`|必需。 采用以下格式指定该应用程序的版本号： `major.minor.build.revision`|  
|`publicKeyToken`|可选。 指定表示最后 8 个字节的 16 字符的十六进制字符串`SHA-1`的应用程序集签名的公钥的哈希值。 使用对目录进行签名的公钥必须为 2048 位或更高版本。<br /><br /> 尽管为程序集签名是可选但建议，但此属性是必需的。 如果程序集未签名，你应从自签名的程序集复制值或使用"虚拟"值均为零。|  
|`processorArchitecture`|必需。 指定的处理器。 有效的值是`msil`适用于所有处理器`x86`的 32 位 Windows`IA64`为 64 位 Windows 和`Itanium`Intel 64 位 Itanium 处理器。|  
|`language`|必需。 标识两个部分语言代码 (例如， `en-US`) 的程序集。 此元素处于`asmv2`命名空间。 如果未指定，默认值是`neutral`。|  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>描述  
 下面的代码示例演示`assemblyIdentity`中的元素[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序清单。 此代码示例摘自[ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)。  
  
### <a name="code"></a>代码  
  
```  
<asmv1:assemblyIdentity   
  name="My Application Deployment.exe"   
  version="1.0.0.0"   
  publicKeyToken="43cb1e8e7a352766"   
  language="neutral"   
  processorArchitecture="x86"   
  type="win32" />  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)   
 [\<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-deployment.md)
