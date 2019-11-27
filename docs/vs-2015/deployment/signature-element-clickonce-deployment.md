---
title: '&lt;签名&gt; 元素（ClickOnce 部署） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <Signature> element [ClickOnce deployment manifest]
ms.assetid: c99b07ad-e8ba-43f2-b0d6-3745e7a7c8b3
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db696546fdd64199753054b38fa2ac554f6a774f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295077"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;签名&gt; 元素（ClickOnce 部署）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含对此部署清单进行数字签名所需的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
      <Signature>   
   XML signature information   
</Signature>  
```  
  
## <a name="remarks"></a>备注  
 使用信封签名对部署清单进行签名是可选的，但建议使用。 有关对 XML 文件进行签名的详细信息，请参阅[http://www.w3.org/TR/xmldsig-core/](https://www.w3.org/TR/xmldsig-core/)中所述的万维网联合会建议 "XML 签名语法和处理"。  
  
 如果要对清单进行签名，则必须为所有文件提供哈希。 无法对包含未进行哈希处理的文件的清单进行签名，因为用户无法验证未经过哈希处理的文件的内容。  
  
## <a name="example"></a>示例  
 下面的代码示例演示了 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署中使用的部署清单中的 `Signature` 元素。  
  
```  
<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">  
  <SignedInfo>  
    <CanonicalizationMethod Algorithm=  
           "http://www.w3.org/TR/2001/REC-xml-c14n-20010315" />  
    <SignatureMethod Algorithm=  
           "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />  
    <Reference URI="">  
      <Transforms>  
        <Transform Algorithm=  
           "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />  
      </Transforms>  
      <DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
      <DigestValue>d2z5AE...</DigestValue>  
    </Reference>  
  </SignedInfo>  
  <SignatureValue>  
4PHj6SaopoLp...  
  </SignatureValue>  
  <KeyInfo>  
    <X509Data>  
      <X509Certificate>  
MIIHnTCCBoWgAwIBAgIKJY9+nwAHAAB...  
      </X509Certificate>  
    </X509Data>  
  </KeyInfo>  
</Signature>  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
