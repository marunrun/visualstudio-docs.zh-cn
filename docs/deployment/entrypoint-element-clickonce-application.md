---
title: '&lt;&gt;)  (ClickOnce 应用程序的入口点元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#commandLine
- urn:schemas-microsoft-com:asm.v2#entryPoint
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <entryPoint> element [ClickOnce application manifest]
- manifests [ClickOnce], entryPoint element
ms.assetid: 10ad3083-10c1-4189-a870-9bba2eab244f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 615a606dc4d04682a9d5a1a69c91b4d2cd67de15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62928615"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;&gt; (ClickOnce 应用程序的入口点元素) 
标识在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 客户端计算机上运行此应用程序时应执行的程序集。

## <a name="syntax"></a>语法

```xml
<entryPoint
   name
>
   <assemblyIdentity
      name
      version
      processorArchitecture
      language
   />
   <commandLine
      file
      parameters
   />
   <customHostRequired />
   <customUX />
</entryPoint>
```

## <a name="elements-and-attributes"></a>元素和属性
 `entryPoint` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v2` 命名空间中。 `entryPoint`在应用程序清单中只能定义一个元素。

 `entryPoint` 元素具有以下属性。

|特性|说明|
|---------------|-----------------|
|`name`|可选。 .NET Framework 不使用此值。|

 `entryPoint` 具有下列元素。

## <a name="assemblyidentity"></a>assemblyIdentity
 必需。 `assemblyIdentity`及其特性的角色是在[ \<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-application.md)中定义的。

 `processorArchitecture`此元素的属性和 `processorArchitecture` `assemblyIdentity` 应用程序清单中其他位置定义的属性必须匹配。

## <a name="commandline"></a>commandLine
 必需。 必须是元素的子 `entryPoint` 元素。 它没有子元素，并且具有以下属性。

| 特性 | 说明 |
|--------------| - |
| `file` | 必需。 对应用程序的启动程序集的本地引用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此值不能包含正斜杠 (/) 或反斜杠 (\\) 路径分隔符。 |
| `parameters` | 必需。 描述要对入口点执行的操作。 唯一有效的值为 `run` ; 如果提供了空白字符串， `run` 则采用。 |

## <a name="customhostrequired"></a>customHostRequired
 可选。 如果包含，则指定此部署包含将在自定义主机内部署的组件，而不是独立应用程序。

 如果此元素存在，则 `assemblyIdentity` 和 `commandLine` 元素不能同时存在。 如果为， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 则在安装过程中将引发验证错误。

 此元素没有属性，没有任何子级。

## <a name="customux"></a>customUX
 可选。 指定应用程序由自定义安装程序安装和维护，并且不创建开始菜单项、快捷方式或 "添加或删除程序" 项。

```xml
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />
```

 包含 customUX 元素的应用程序必须提供一个使用类的自定义安装程序 <xref:System.Deployment.Application.InPlaceHostingManager> 来执行安装操作。 使用此元素的应用程序不能通过双击其清单或 setup.exe 必备组件引导程序来安装。 自定义安装程序可以创建开始菜单项、快捷方式以及 "添加或删除程序" 项。 如果自定义安装程序不创建 "添加或删除程序" 项，则它必须存储属性提供的订阅标识符， <xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A> 并使用户能够在以后通过调用方法来卸载应用程序 <xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A> 。 有关详细信息，请参阅 [演练：为 ClickOnce 应用程序创建自定义安装](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)程序。

## <a name="remarks"></a>备注
 此元素标识应用程序的程序集和入口点 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

 不能使用在 `commandLine` 运行时将参数传递到应用程序。 可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从应用程序的部署访问查询字符串参数 <xref:System.AppDomain> 。 有关详细信息，请参阅 [如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。

## <a name="example"></a>示例
 下面的代码示例演示应用程序的 `entryPoint` 应用程序清单中的元素 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 此代码示例是为 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md) 主题提供的更大示例的一部分。

```xml
<!-- Identify the main code entrypoint. -->
<!-- This code runs the main method in an executable assembly. -->
  <entryPoint>
    <assemblyIdentity
      name="MyApplication"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="x86" />
    <commandLine file="MyApplication.exe" parameters="" />
  </entryPoint>
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
