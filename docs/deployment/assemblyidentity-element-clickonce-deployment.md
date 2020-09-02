---
title: '&lt;&gt; (ClickOnce 部署) 的 assemblyIdentity 元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce deployment manifest]
ms.assetid: f4a3bb83-c800-47d0-9905-9a5ae2486838
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 56525cc0c0c754a7fa3a1f4c2c5b6cf2e941e9b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62929057"
---
# <a name="ltassemblyidentitygt-element-clickonce-deployment"></a>&lt;&gt; (ClickOnce 部署的 assemblyIdentity 元素) 
标识应用程序的主要程序集 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

## <a name="syntax"></a>语法

```xml

      <assemblyIdentity  
   name 
   version
   publicKeyToken
   processorArchitecture
    type
/>
```

## <a name="elements-and-attributes"></a>元素和属性
 `assemblyIdentity` 元素是必需的。 它不包含任何子元素，并且具有以下属性。

|特性|说明|
|---------------|-----------------|
|`name`|必需。 标识用于提供信息的部署的用户可读名称。<br /><br /> 如果 `name` 包含特殊字符（如单引号或双引号），则应用程序可能无法激活。|
|`version`|必需。 用以下格式指定程序集的版本号： `major.minor.build.revision` 。<br /><br /> 此值必须在更新的清单中递增才能触发应用程序更新。|
|`publicKeyToken`|必需。 指定16个字符的十六进制字符串，该字符串表示用于对部署清单进行签名的公钥的 SHA-1 哈希值的最后8个字节。 用于签名的公钥必须是2048或更高版本。<br /><br /> 尽管建议为程序集签名，但这是可选的，但此属性是必需的。 如果程序集是无符号的，则应从自签名的程序集复制一个值，或使用 "虚拟" 值全部为零。|
|`processorArchitecture`|必需。 指定处理器。 有效值适用于 `msil` 所有处理器，适用于 `x86` 32 位 windows， `IA64` 适用于64位 windows， `Itanium` 适用于 Intel 64 位 Itanium 处理器。|
|`type`|必需。 与 Windows 并行安装技术的兼容性。 唯一允许的值为 `win32` 。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的代码示例演示了 `assemblyIdentity` 部署清单中的元素 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此代码示例是为 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md) 主题提供的更大示例的一部分。

```xml
<!-- Identify the deployment. -->
<assemblyIdentity
  name="My Application Deployment.app"
  version="1.0.0.0"
  publicKeyToken="43cb1e8e7a352766"
  language="neutral"
  processorArchitecture="x86"
  xmlns="urn:schemas-microsoft-com:asm.v1" />
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
- [\<assemblyIdentity> element](../deployment/assemblyidentity-element-clickonce-application.md)