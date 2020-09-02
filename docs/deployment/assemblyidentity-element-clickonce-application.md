---
title: '&lt;&gt; (ClickOnce 应用程序) 的 assemblyIdentity 元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce application manifest]
ms.assetid: f48e9531-efac-4d11-8166-f63a5ece1ac5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7870fcf644103ec7f048a809e439cb962f63bd07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900662"
---
# <a name="ltassemblyidentitygt-element-clickonce-application"></a>&lt;&gt; (ClickOnce 应用程序的 assemblyIdentity 元素) 
标识部署中部署的应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

## <a name="syntax"></a>语法

```xml

      <assemblyIdentity
   name
   version
   publicKeyToken
   processorArchitecture
   language
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assemblyIdentity` 元素是必需的。 它不包含任何子元素，并且具有以下属性。

|特性|说明|
|---------------|-----------------|
|`Name`|必需。 标识应用程序的名称。<br /><br /> 如果 `Name` 包含特殊字符（如单引号或双引号），则应用程序可能无法激活。|
|`Version`|必需。 按以下格式指定应用程序的版本号： `major.minor.build.revision`|
|`publicKeyToken`|可选。 指定16个字符的十六进制字符串，该字符串表示 `SHA-1` 用于对应用程序或程序集进行签名的公钥的哈希值的最后8个字节。 用于对目录进行签名的公钥必须是2048或更高版本。<br /><br /> 尽管建议为程序集签名，但这是可选的，但此属性是必需的。 如果程序集是无符号的，则应从自签名的程序集复制一个值，或使用 "虚拟" 值全部为零。|
|`processorArchitecture`|必需。 指定处理器。 有效值适用于 `msil` 所有处理器，适用于 `x86` 32 位 windows， `IA64` 适用于64位 windows， `Itanium` 适用于 Intel 64 位 Itanium 处理器。|
|`language`|必需。 标识程序集的两部分语言代码 (例如 `en-US`) 。 此元素位于 `asmv2` 命名空间中。 如果未指定，则默认值为 `neutral` 。|

## <a name="examples"></a>示例

### <a name="description"></a>说明
 下面的代码示例演示 `assemblyIdentity` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中的元素。 此代码示例是 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<asmv1:assemblyIdentity
  name="My Application Deployment.exe"
  version="1.0.0.0"
  publicKeyToken="43cb1e8e7a352766"
  language="neutral"
  processorArchitecture="x86"
  type="win32" />
```

## <a name="see-also"></a>请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<assemblyIdentity> element](../deployment/assemblyidentity-element-clickonce-deployment.md)