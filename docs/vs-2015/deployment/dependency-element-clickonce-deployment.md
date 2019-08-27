---
title: '&lt;依赖项&gt;元素 （ClickOnce 部署） |Microsoft Docs'
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
- <dependency> element [ClickOnce deployment manifest]
ms.assetid: 9b4d2082-0347-4922-ac70-85f11b913039
caps.latest.revision: 29
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f191b11dfce5b3877d0a31e260e092000a556a5a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187784"
---
# <a name="ltdependencygt-element-clickonce-deployment"></a>&lt;依赖项&gt;元素 （ClickOnce 部署）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识要安装，应用程序的版本和应用程序清单的位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
      <dependency>   
   <dependentAssembly  
      preRequisite  
      visible  
      dependencyType  
      codeBase  
      size  
   >   
      <assemblyIdentity   
         name   
         version   
         publicKeyToken   
         processorArchitecture   
         language  
         type  
      />   
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
  
   </dependentAssembly>   
</dependency>  
```  
  
## <a name="elements-and-attributes"></a>元素和属性  
 `dependency`元素是必需的。 它没有任何属性。 部署清单可以有多个`dependency`元素。  
  
 `dependency`元素通常表示程序集包含在中的主应用程序依赖项[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 如果 Main.exe 应用程序使用名为 DotNetAssembly.dll 程序集，则必须在依赖项部分列出该程序集。 依赖关系，但是，也可以表示其他类型的依赖项，如依赖特定版本的公共语言运行时，全局程序集缓存 (GAC) 中的程序集或 COM 对象。 因为它是一种无人参与部署技术，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]无法启动下载和安装这些类型的依赖项，但它不会阻止运行该应用程序如果不存在一个或多个指定的依赖项。  
  
## <a name="dependentassembly"></a>dependentAssembly  
 必需。 此元素包含`assemblyIdentity`元素。 下表显示了属性`dependentAssembly`支持。  
  
|特性|描述|  
|---------------|-----------------|  
|`preRequisite`|可选。 指定此程序集应已存在于 gac。 有效值为 `true` 和 `false`。 如果`true`，并在 GAC 中不存在指定的程序集、 应用程序无法运行。|  
|`visible`|可选。 标识顶级应用程序标识，包括其依赖项。 在内部使用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]来管理应用程序存储和激活。|  
|`dependencyType`|必需。 此依赖项和应用程序之间的关系。 有效值为：<br /><br /> -   `install`. 组件表示从当前应用程序的单独安装。<br />-   `preRequisite`. 组件被必需的当前应用程序。|  
|`codebase`|可选。 应用程序清单的完整路径。|  
|`size`|可选。 应用程序清单，以字节为单位的大小。|  
  
## <a name="assemblyidentity"></a>assemblyIdentity  
 必需。 此元素是 `dependentAssembly` 元素的子元素。 内容`assemblyIdentity`必须是与中所述相同[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序清单。 下表显示的属性`assemblyIdentity`元素。  
  
|特性|描述|  
|---------------|-----------------|  
|`Name`|必需。 标识应用程序的名称。|  
|`Version`|必需。 采用以下格式指定该应用程序的版本号： `major.minor.build.revision`|  
|`publicKeyToken`|必需。 指定的 16 字符十六进制字符串表示应用程序集签名的公钥的 sha-1 哈希的最后 8 个字节。 用于签名的公钥必须为 2048 位或更高版本。|  
|`processorArchitecture`|必需。 指定微处理器。 有效的值是`x86`的 32 位 Windows 和`IA64`的 64 位 Windows。|  
|`Language`|可选。 标识程序集的两个部分语言代码。 例如，EN-US，代表对于英语 （美国）。 默认值为 `neutral`。 此元素处于`asmv2`命名空间。|  
|`type`|可选。 有关向后兼容性 Windows 并行安装技术。 唯一允许的值是`win32`。|  
  
## <a name="hash"></a>hash  
 `hash`元素是可选的子`file`元素。 `hash` 元素没有属性。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用应用程序中的所有文件的哈希算法作为安全检查以确保部署之后没有任何文件发生更改。 如果`hash`元素不包含，不会执行此检查。 因此，省略`hash`不建议元素。  
  
## <a name="dsigtransforms"></a>dsig:Transforms  
 `dsig:Transforms`元素是必需的子`hash`元素。 `dsig:Transforms` 元素没有属性。  
  
## <a name="dsigtransform"></a>dsig:Transform  
 `dsig:Transform`元素是必需的子`dsig:Transforms`元素。 下表显示的属性`dsig:Transform`元素。  
  
|特性|描述|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件的摘要算法。 当前使用的唯一值[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]是`urn:schemas-microsoft-com:HashTransforms.Identity`。|  
  
## <a name="dsigdigestmethod"></a>dsig:DigestMethod  
 `dsig:DigestMethod`元素是必需的子`hash`元素。 下表显示的属性`dsig:DigestMethod`元素。  
  
|特性|描述|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件的摘要算法。 当前使用的唯一值[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]是`http://www.w3.org/2000/09/xmldsig#sha1`。|  
  
## <a name="dsigdigestvalue"></a>dsig:DigestValue  
 `dsig:DigestValue`元素是必需的子`hash`元素。 `dsig:DigestValue` 元素没有属性。 其文本值为指定的文件的计算哈希值。  
  
## <a name="remarks"></a>备注  
 部署清单进行签名通常具有单个`assemblyIdentity`元素，它标识的名称和版本的应用程序清单。  
  
## <a name="example"></a>示例  
 下面的代码示例演示`dependency`中的元素[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署清单。  
  
```  
<!-- Identify the assembly dependencies -->  
<dependency>  
  <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="16384">  
    <assemblyIdentity name="MyApplication" version="0.0.0.0" cultural="neutral" processorArchitecture="msil" />  
    <hash>  
      <dsig:Transforms>  
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
      </dsig:Transforms>  
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
       <dsig:DigestValue>YzXYZJAvj9pgAG3y8jXUjC7AtHg=</dsig:DigestValue>  
    </hash>  
  </dependentAssembly>  
</dependency>  
```  
  
## <a name="example"></a>示例  
 下面的代码示例指定对已安装到 GAC 中程序集的依赖项。  
  
```  
<dependency>  
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
    <assemblyIdentity name="GACAssembly" version="1.0.0.0" language="neutral" processorArchitecture="msil" />  
  </dependentAssembly>  
</dependency>  
```  
  
## <a name="example"></a>示例  
 下面的代码示例指定公共语言运行时的特定版本的依赖项。  
  
```  
<dependency>  
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
    <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50215.0" />  
  </dependentAssembly>  
</dependency>  
```  
  
## <a name="example"></a>示例  
 下面的代码示例指定操作系统依赖项。  
  
```  
<dependency>  
   <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">  
      <osVersionInfo>  
         <os majorVersion="4" minorVersion="10" />  
      </osVersionInfo>  
   </dependentOS>  
</dependency>  
```  
  
## <a name="see-also"></a>请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [\<dependency> 元素](../deployment/dependency-element-clickonce-application.md)
