---
title: '&lt;依赖项&gt;元素 （ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#osVersionInfo
- urn:schemas-microsoft-com:asm.v2#os
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#dependency
- http://www.w3.org/2000/09/xmldsig#DigestValue
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
- urn:schemas-microsoft-com:asm.v2#dependentAssembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- manifests [ClickOnce], dependency element
- <dependency> element [ClickOnce application manifest]
ms.assetid: 09d6a1e0-60f8-4fbd-843b-8e49ee3115a3
caps.latest.revision: 36
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e79fadcab1a4f00c084d675c3267b5886772fe2c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199882"
---
# <a name="ltdependencygt-element-clickonce-application"></a>&lt;依赖项&gt;元素 （ClickOnce 应用程序）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识应用程序所需的平台或程序集依赖项。  
  
## <a name="syntax"></a>语法  
  
```  
  
      <dependency>  
   <dependentOS  
      supportURL  
      description  
   >  
      <osVersionInfo>  
         <os  
            majorVersion  
            minorVersion  
            buildNumber  
            servicePackMajor  
            servicePackMinor  
            productType  
            suiteType  
         />   
      </osVersionInfo>  
   </dependentOS>  
   <dependentAssembly  
      dependencyType  
      allowDelayedBinding  
      group  
      codeBase  
      size  
   >  
      <assemblyIdentity  
         name  
         version  
         processorArchitecture  
         language  
      >  
         <hash>  
            <dsig:Transforms>  
               <dsig:Transform  
                  Algorithm  
            />  
            </dsig:Transforms>  
            <dsig:DigestMethod />  
            <dsig:DigestValue>  
            </dsig:DigestValue>  
    </hash>  
  
      </assemblyIdentity>  
   </dependentAssembly>  
</dependency>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `dependency`元素是必需的。 可能有多个实例`dependency`相同的应用程序清单中。  
  
 `dependency`元素没有属性，并包含以下子元素。  
  
### <a name="dependentos"></a>dependentOS  
 可选。 包含`osVersionInfo`元素。 `dependentOS`并`dependentAssembly`元素是互斥的： 一个或另一个必须存在`dependency`元素，但不是能同时。  
  
 `dependentOS` 支持以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`supportUrl`|可选。 指定依赖于平台的支持 URL。 如果找到所需的平台，将向用户显示此 URL。|  
|`description`|可选。 介绍了用户可读的窗体中所描述的操作系统`dependentOS`元素。|  
  
### <a name="osversioninfo"></a>osVersionInfo  
 必需。 此元素是 `dependentOS` 元素的子元素，并且包含 `os` 元素。 此元素没有属性。  
  
### <a name="os"></a>操作系统  
 必需。 此元素是 `osVersionInfo` 元素的子元素。 此元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`majorVersion`|必需。 指定操作系统的主版本号。|  
|`minorVersion`|必需。 指定操作系统的次版本号。|  
|`buildNumber`|必需。 指定的 os 内部版本号。|  
|`servicePackMajor`|必需。 指定 service pack 的操作系统的主版本号。|  
|`servicePackMinor`|可选。 指定 service pack 的操作系统的次版本号。|  
|`productType`|可选。 标识产品类型值。 有效值为 `server`、`workstation` 和 `domainController`。 例如，对于 Windows 2000 Professional，此属性的值是`workstation`。|  
|`suiteType`|可选。 标识系统或系统的配置类型上可用的产品套件。 有效值为 `backoffice`、`blade`、`datacenter`、`enterprise`、`home`、`professional`、`smallbusiness`、`smallbusinessRestricted` 和 `terminal`。 例如，对于 Windows 2000 Professional，此属性的值是`professional`。|  
  
### <a name="dependentassembly"></a>dependentAssembly  
 可选。 包含`assemblyIdentity`元素。 `dependentOS`并`dependentAssembly`元素是互斥的： 一个或另一个必须存在`dependency`元素，但不是能同时。  
  
 `dependentAssembly` 具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`dependencyType`|必需。 指定的依赖关系类型。 有效值为 `preprequisite` 和 `install`。 `install`的一部分安装的程序集[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 一个`prerequisite`程序集必须位于全局程序集缓存 (GAC) 之前[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]可以安装应用程序。|  
|`allowDelayedBinding`|必需。 指定是否可以在运行时以编程方式加载程序集。|  
|`group`|可选。 如果`dependencyType`属性设置为`install`，指定该仅按需安装的程序集的命名的组。 有关详细信息，请参见[演练：在设计器中使用 ClickOnce 部署 API 按需下载程序集](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)。<br /><br /> 如果设置为`framework`并`dependencyType`属性设置为`prerequisite`，将该程序集指定为.NET Framework 的一部分。 全局程序集缓存 (GAC) 时不会检查此程序集安装在[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]及更高版本。|  
|`codeBase`|时需要`dependencyType`属性设置为`install`。 依赖程序集的路径。 可以是绝对路径或相对路径的清单代码基。 此路径必须是为了使程序集清单是有效的 URI 有效。|  
|`size`|时需要`dependencyType`属性设置为`install`。 依赖程序集，以字节为单位的大小。|  
  
### <a name="assemblyidentity"></a>assemblyIdentity  
 必需。 此元素是 `dependentAssembly` 元素的子元素，并且包含下列元素。  
  
|特性|描述|  
|---------------|-----------------|  
|`name`|必需。 标识应用程序的名称。|  
|`version`|必需。 采用以下格式指定该应用程序的版本号： `major.minor.build.revision`|  
|`publicKeyToken`|可选。 指定表示最后 8 个字节的 16 字符的十六进制字符串`SHA-1`的应用程序集签名的公钥的哈希值。 使用对目录进行签名的公钥必须是 2048 位或的详细信息。|  
|`processorArchitecture`|可选。 指定的处理器。 有效的值是`x86`的 32 位 Windows 和`I64`的 64 位 Windows。|  
|`language`|可选。 标识的两个部分语言代码，如 EN-US，程序集。|  
  
### <a name="hash"></a>hash  
 `hash`元素是可选的子`assemblyIdentity`元素。 `hash` 元素没有属性。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用应用程序中的所有文件的哈希算法作为安全检查，以确保部署之后没有任何文件发生更改。 如果`hash`元素不包含，不会执行此检查。 因此，省略`hash`不建议元素。  
  
### <a name="dsigtransforms"></a>dsig:Transforms  
 `dsig:Transforms`元素是必需的子`hash`元素。 `dsig:Transforms` 元素没有属性。  
  
### <a name="dsigtransform"></a>dsig:Transform  
 `dsig:Transform`元素是必需的子`dsig:Transforms`元素。 `dsig:Transform` 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件的摘要算法。 当前使用的唯一值[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]是`urn:schemas-microsoft-com:HashTransforms.Identity`。|  
  
### <a name="dsigdigestmethod"></a>dsig:DigestMethod  
 `dsig:DigestMethod`元素是必需的子`hash`元素。 `dsig:DigestMethod` 元素具有以下属性。  
  
|特性|描述|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件的摘要算法。 当前使用的唯一值[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]是`http://www.w3.org/2000/09/xmldsig#sha1`。|  
  
### <a name="dsigdigestvalue"></a>dsig:DigestValue  
 `dsig:DigestValue`元素是必需的子`hash`元素。 `dsig:DigestValue` 元素没有属性。 其文本值为指定的文件的计算哈希值。  
  
## <a name="remarks"></a>备注  
 你的应用程序所使用的所有程序集必须具有相应`dependency`元素。 依赖程序集不包含必须作为预安装在全局程序集缓存中平台程序集的程序集。  
  
## <a name="example"></a>示例  
 下面的代码示例演示`dependency`中的元素[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序清单。 此代码示例是为提供一个更大示例的一部分[ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)主题。  
  
```  
<dependency>  
  <dependentOS>  
    <osVersionInfo>  
      <os   
        majorVersion="4"   
        minorVersion="10"   
        buildNumber="0"   
        servicePackMajor="0" />  
    </osVersionInfo>  
  </dependentOS>  
</dependency>  
<dependency>  
  <dependentAssembly  
    dependencyType="preRequisite"  
    allowDelayedBinding="true">  
    <assemblyIdentity  
      name="Microsoft.Windows.CommonLanguageRuntime"  
      version="4.0.20506.0" />  
  </dependentAssembly>  
</dependency>  
  
<dependency>  
  <dependentAssembly  
    dependencyType="install"  
    allowDelayedBinding="true"  
    codebase="MyApplication.exe"  
    size="4096">  
    <assemblyIdentity  
      name="MyApplication"  
      version="1.0.0.0"  
      language="neutral"  
      processorArchitecture="x86" />  
    <hash>  
      <dsig:Transforms>  
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
      </dsig:Transforms>  
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
      <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>  
    </hash>  
  </dependentAssembly>  
</dependency>  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)   
 [\<dependency> 元素](../deployment/dependency-element-clickonce-deployment.md)
