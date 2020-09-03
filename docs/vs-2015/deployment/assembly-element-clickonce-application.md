---
title: '&lt;&gt; (ClickOnce 应用程序) 的 assembly 元素 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce application manifest]
ms.assetid: 51410569-10f9-4c0a-96b5-d39185edbefc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d619b8b3cd81e5b00fc689077a95ade08f4d7eed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183481"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;&gt; (ClickOnce 应用程序的 assembly 元素) 
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

应用程序清单的顶级元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
      <assembly  
   manifestVersion  
/>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `assembly`元素为根元素，并且是必需的。 它包含的第一个元素必须是 `assemblyIdentity` 元素。 清单元素必须位于以下命名空间之一中：  
  
 `urn:schemas-microsoft-com:asm.v1`  
  
 `urn:schemas-microsoft-com:asm.v2`  
  
 `http://www.w3.org/2000/09/xmldsig#`  
  
 程序集的子元素也必须在这些命名空间中通过继承或标记。  
  
 `assembly` 元素具有以下属性。  
  
|特性|说明|  
|---------------|-----------------|  
|`manifestVersion`|必需。 `manifestVersion`特性必须设置为 `1.0` 。|  
  
## <a name="example"></a>示例  
 下面的代码示例演示应用程序的 `assembly` 应用程序清单中的元素 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。 此代码示例是 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)中提供的一个更大示例的一部分。  
  
```  
<asmv1:assembly   
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"   
  manifestVersion="1.0"   
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"  
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#  
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"  
  xmlns="urn:schemas-microsoft-com:asm.v2"  
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"  
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"  
  xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance  
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">  
```  
  
## <a name="see-also"></a>另请参阅  
 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)   
 [\<assembly> 元素](../deployment/assembly-element-clickonce-deployment.md)
