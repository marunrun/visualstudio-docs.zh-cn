---
title: '&lt;&gt; (ClickOnce 部署) 的 publisherIdentity 元素 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 486e0bc5059e041f02e8dac4836c5ff59b27f63e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157639"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;&gt; (ClickOnce 部署的 publisherIdentity 元素) 
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含有关为此部署清单签名的发布者的信息。  
  
## <a name="syntax"></a>语法  
  
```  
<publisherIdentity  
   name  
   issuerKeyHash  
/>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `publisherIdentity`签名清单需要元素。 下表显示 `publisherIdentity` 元素支持的属性。  
  
|特性|说明|  
|---------------|-----------------|  
|`name`|必需。 描述发布此应用程序的参与方的标识。|  
|`issuerKeyHash`|必需。 包含证书颁发者的公钥的 SHA-1 哈希。|  
  
#### <a name="parameters"></a>参数  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
  
## <a name="subhead"></a>副标题
