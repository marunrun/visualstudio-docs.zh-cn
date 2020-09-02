---
title: '&lt;&gt; (ClickOnce 部署) 的 compatibleFrameworks 元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99db3d51414197df469aaa2eabe97e0967c31b05
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66746029"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;&gt; (ClickOnce 部署的 compatibleFrameworks 元素) 
标识此应用程序可在其上安装和运行的 .NET Framework 版本。

> [!NOTE]
> [*MageUI.exe*](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client) `compatibleFrameworks` 使用[*MageUI.exe*](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)保存已使用证书签名的应用程序清单时，MageUI.exe不支持元素。 相反，您必须使用 [*Mage.exe*](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)。

## <a name="syntax"></a>语法

```xml
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
 `compatibleFrameworks`对于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 以 .NET Framework 4 或更高版本提供的运行时为目标的部署清单，该元素是必需的。 `compatibleFrameworks`元素包含一个或多个 `framework` 元素，这些元素指定此应用程序可在其上运行的 .NET Framework 版本。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]运行时将运行此列表中第一个可用的应用程序 `framework` 。

 下表列出了元素支持的属性 `compatibleFrameworks` 。

|特性|说明|
|---------------|-----------------|
|`S` `upportUrl`|可选。 指定可在其中下载首选兼容 .NET Framework 版本的 URL。|

## <a name="framework"></a>框架
 必需。 下表列出了元素支持的属性 `framework` 。

|特性|说明|
|---------------|-----------------|
|`targetVersion`|必需。 指定目标 .NET Framework 的版本号。|
|`profile`|必需。 指定目标 .NET Framework 的配置文件。|
|`supportedRuntime`|必需。 指定与目标 .NET Framework 关联的运行时的版本号。|

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 下面的代码示例演示了 `compatibleFrameworks` 部署清单中的元素 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此部署可以在上运行 [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] 。 它还可以在 .NET Framework 4 上运行，因为它是的超集 [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] 。

```xml
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">
  <framework
      targetVersion="4.0"
      profile="Client"
      supportedRuntime="4.0.30319" />
</compatibleFrameworks>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)