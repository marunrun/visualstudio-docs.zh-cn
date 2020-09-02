---
title: '&lt;&gt; (ClickOnce 部署) 的依赖关系元素 |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187784"
---
# <a name="ltdependencygt-element-clickonce-deployment"></a>&lt;&gt;ClickOnce 部署 (依赖关系元素) 
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

标识要安装的应用程序的版本以及应用程序清单的位置。  
  
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
 `dependency` 元素是必需的。 它没有属性。 部署清单可以有多个 `dependency` 元素。  
  
 `dependency`元素通常表示应用程序中包含的程序集上主应用程序的依赖项 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。 如果 Main.exe 应用程序使用名为 DotNetAssembly.dll 的程序集，则该程序集必须在依赖项部分中列出。 不过，依赖项还可以表示其他类型的依赖项，例如公共语言运行时的特定版本、全局程序集缓存中的程序集 (GAC) 或 COM 对象上的依赖项。 由于它是一种无接触部署技术，因此 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 无法启动这些类型的依赖项的下载和安装，但如果一个或多个指定的依赖项不存在，则它会阻止应用程序运行。  
  
## <a name="dependentassembly"></a>dependentAssembly  
 必需。 此元素包含 `assemblyIdentity` 元素。 下表显示了支持的属性 `dependentAssembly` 。  
  
|特性|说明|  
|---------------|-----------------|  
|`preRequisite`|可选。 指定此程序集应已存在于 GAC 中。 有效值为 `true` 和 `false`。 如果 `true` 和 GAC 中不存在指定的程序集，则该应用程序将无法运行。|  
|`visible`|可选。 标识顶级应用程序标识，包括其依赖项。 供内部使用， [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 以管理应用程序存储和激活。|  
|`dependencyType`|必需。 此依赖项与应用程序之间的关系。 有效值是：<br /><br /> -   `install`. 组件表示来自当前应用程序的单独安装。<br />-   `preRequisite`. 组件是当前应用程序所必需的。|  
|`codebase`|可选。 应用程序清单的完整路径。|  
|`size`|可选。 应用程序清单的大小（以字节为单位）。|  
  
## <a name="assemblyidentity"></a>assemblyIdentity  
 必需。 此元素是 `dependentAssembly` 元素的子元素。 的内容 `assemblyIdentity` 必须与应用程序清单中所述相同 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。 下表显示了元素的属性 `assemblyIdentity` 。  
  
|特性|说明|  
|---------------|-----------------|  
|`Name`|必需。 标识应用程序的名称。|  
|`Version`|必需。 指定应用程序的版本号，格式如下： `major.minor.build.revision`|  
|`publicKeyToken`|必需。 指定16个字符的十六进制字符串，该字符串表示应用程序或程序集签名时所用公钥的 SHA-1 哈希值的最后8个字节。 用于签名的公钥必须为2048位或更大。|  
|`processorArchitecture`|必需。 指定微处理器。 有效值 `x86` 适用于32位 windows 和 `IA64` 64 位 windows。|  
|`Language`|可选。 标识程序集的两部分语言代码。 例如，EN-US 表示美国英语 () 。 默认值为 `neutral`。 此元素位于 `asmv2` 命名空间中。|  
|`type`|可选。 为了向后兼容 Windows 并行安装技术。 唯一允许的值为 `win32` 。|  
  
## <a name="hash"></a>hash  
 `hash`元素是元素的可选子元素 `file` 。 `hash` 元素没有属性。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用应用程序中所有文件的算法哈希作为安全检查，以确保在部署后没有任何文件发生更改。 如果 `hash` 不包含该元素，则不会执行此检查。 因此， `hash` 不建议省略元素。  
  
## <a name="dsigtransforms"></a>dsig:Transforms  
 `dsig:Transforms`元素是元素的必需子元素 `hash` 。 `dsig:Transforms` 元素没有属性。  
  
## <a name="dsigtransform"></a>dsig:Transform  
 `dsig:Transform`元素是元素的必需子元素 `dsig:Transforms` 。 下表显示了元素的属性 `dsig:Transform` 。  
  
|特性|说明|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件摘要的算法。 目前使用的唯一值 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 是 `urn:schemas-microsoft-com:HashTransforms.Identity` 。|  
  
## <a name="dsigdigestmethod"></a>dsig:DigestMethod  
 `dsig:DigestMethod`元素是元素的必需子元素 `hash` 。 下表显示了元素的属性 `dsig:DigestMethod` 。  
  
|特性|说明|  
|---------------|-----------------|  
|`Algorithm`|用于计算此文件摘要的算法。 目前使用的唯一值 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 是 `http://www.w3.org/2000/09/xmldsig#sha1` 。|  
  
## <a name="dsigdigestvalue"></a>dsig:DigestValue  
 `dsig:DigestValue`元素是元素的必需子元素 `hash` 。 `dsig:DigestValue` 元素没有属性。 它的文本值为指定文件的计算所得的哈希值。  
  
## <a name="remarks"></a>备注  
 部署清单通常具有单个 `assemblyIdentity` 元素，用于标识应用程序清单的名称和版本。  
  
## <a name="example"></a>示例  
 下面的代码示例演示了 `dependency` 部署清单中的元素 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。  
  
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
 下面的代码示例指定对 GAC 中已安装的程序集的依赖关系。  
  
```  
<dependency>  
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
    <assemblyIdentity name="GACAssembly" version="1.0.0.0" language="neutral" processorArchitecture="msil" />  
  </dependentAssembly>  
</dependency>  
```  
  
## <a name="example"></a>示例  
 下面的代码示例指定公共语言运行时特定版本的依赖项。  
  
```  
<dependency>  
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
    <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50215.0" />  
  </dependentAssembly>  
</dependency>  
```  
  
## <a name="example"></a>示例  
 下面的代码示例指定了一个操作系统依赖项。  
  
```  
<dependency>  
   <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">  
      <osVersionInfo>  
         <os majorVersion="4" minorVersion="10" />  
      </osVersionInfo>  
   </dependentOS>  
</dependency>  
```  
  
## <a name="see-also"></a>另请参阅  
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [\<dependency> 元素](../deployment/dependency-element-clickonce-application.md)
