---
title: '&lt;签名&gt;元素 （ClickOnce 部署） |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <Signature> element [ClickOnce deployment manifest]
ms.assetid: c99b07ad-e8ba-43f2-b0d6-3745e7a7c8b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c636a4178cf278c2bb0ad75f4e78b94758dda30
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62927483"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;签名&gt;元素 （ClickOnce 部署）
包含对此部署清单进行数字签名所需的信息。

## <a name="syntax"></a>语法

```xml

      <Signature> 
   XML signature information 
</Signature>
```

## <a name="remarks"></a>备注
 使用封装签名的部署清单签名是可选的但建议。 有关对 XML 文件进行签名的详细信息，请参阅 World Wide Web 联合会建议"Xml-signature Syntax and Processing，"中所述[ http://www.w3.org/TR/xmldsig-core/ ](http://www.w3.org/TR/xmldsig-core/)。

 如果你想要对清单签名，哈希必须提供的所有文件。 具有不哈希处理的文件的清单不能进行签名，因为用户不能验证未经哈希的文件的内容。

## <a name="example"></a>示例
 下面的代码示例演示`Signature`元素中使用的部署清单中[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署。

```xml
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
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)