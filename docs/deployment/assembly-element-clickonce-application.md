---
title: '&lt;程序集&gt;元素 （ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce application manifest]
ms.assetid: 51410569-10f9-4c0a-96b5-d39185edbefc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b629243920021adc3833f43f268f05638029dc7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900755"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;程序集&gt;元素 （ClickOnce 应用程序）
应用程序清单的的顶级元素。

## <a name="syntax"></a>语法

```xml

      <assembly
   manifestVersion
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assembly`元素是根元素，是必需的。 它包含的第一个元素必须是`assemblyIdentity`元素。 清单元素必须采用以下命名空间之一：

 `urn:schemas-microsoft-com:asm.v1`

 `urn:schemas-microsoft-com:asm.v2`

 `http://www.w3.org/2000/09/xmldsig#`

 程序集的子元素也必须通过继承或使用标记，这些命名空间中。

 `assembly` 元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`manifestVersion`|必需。 `manifestVersion`属性必须设置为`1.0`。|

## <a name="example"></a>示例
 下面的代码示例演示`assembly`元素中的应用程序清单[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序。 此代码示例摘自[ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)。

```xml
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

## <a name="see-also"></a>请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<assembly> 元素](../deployment/assembly-element-clickonce-deployment.md)
