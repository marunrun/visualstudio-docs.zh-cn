---
title: '&lt;入口点&gt;元素 （ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9ce9fcbddf54dff0ee8574d0c2a5a3df4d8b5c7e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193496"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;入口点&gt;元素 （ClickOnce 应用程序）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识应为程序集时执行此[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]客户端计算机上运行应用程序。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 `entryPoint` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v2` 命名空间中。 只能有一个`entryPoint`应用程序清单中定义的元素。  
  
 `entryPoint` 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`name`|可选。 .NET Framework 不使用此值。|  
  
 `entryPoint` 具有下列元素。  
  
## <a name="assemblyidentity"></a>assemblyIdentity  
 必需。 角色`assemblyIdentity`，其属性的定义[ \<assemblyIdentity > 元素](../deployment/assemblyidentity-element-clickonce-application.md)。  
  
 `processorArchitecture`此元素的属性和`processorArchitecture`属性中定义`assemblyIdentity`其他位置中应用程序清单必须匹配。  
  
## <a name="commandline"></a>commandLine  
 必需。 必须是子元素的`entryPoint`元素。 它不包含任何子元素，并具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`file`|必需。 启动程序集的本地引用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 此值不能包含正斜杠 （/） 或反斜杠 (\\) 路径分隔符。|  
|`parameters`|必需。 描述要执行的入口点的操作。 唯一有效的值是`run`; 如果提供空字符串，则`run`假定。|  
  
## <a name="customhostrequired"></a>customHostRequired  
 可选。 如果包含，指定此部署包含将在自定义主机内部署的组件，也不是独立的应用程序。  
  
 如果存在，此元素`assemblyIdentity`和`commandLine`元素也必须存在。 如果是，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]在安装过程中，将引发验证错误。  
  
 此元素不具有属性和任何子级。  
  
## <a name="customux"></a>customUX  
 可选。 指定的应用程序安装和维护的自定义安装程序，并且不会不创建开始菜单项、 快捷方式或添加或删除程序条目。  
  
```  
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />  
```  
  
 包括 customUX 元素的应用程序必须提供自定义安装程序，则使用<xref:System.Deployment.Application.InPlaceHostingManager>类来执行安装操作。 不能通过双击其清单或 setup.exe 先决条件引导程序安装的应用程序与此元素。 自定义安装程序可以创建开始菜单项、 快捷方式，以及添加或删除程序条目。 如果自定义安装程序不会创建一个添加或删除程序条目，它必须将存储提供的订阅标识符<xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A>属性，并使用户更高版本卸载该应用程序，通过调用<xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A>方法。 有关详细信息，请参见[演练：创建 ClickOnce 应用程序的自定义安装程序](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)。  
  
## <a name="remarks"></a>备注  
 此元素标识的程序集和入口点[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。  
  
 不能使用`commandLine`将参数传递到你的应用程序在运行时。 您可以访问的查询字符串参数[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]从应用程序的部署<xref:System.AppDomain>。 有关详细信息，请参阅[如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例演示`entryPoint`元素中的应用程序清单[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 此代码示例是为提供一个更大示例的一部分[ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)主题。  
  
```  
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
  
## <a name="see-also"></a>请参阅  
 [ndptecclick](../deployment/clickonce-application-manifest.md)
