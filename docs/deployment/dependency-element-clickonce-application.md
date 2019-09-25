---
title: '&lt;dependency&gt;元素（ClickOnce 应用程序） |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3aa949aa2f8e718ab0209c54a0ea2160c042a4eb
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71252484"
---
# <a name="ltdependencygt-element-clickonce-application"></a>&lt;dependency&gt;元素（ClickOnce 应用程序）
标识应用程序所需的平台或程序集依赖项。

## <a name="syntax"></a>语法

```xml

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
 元素`dependency`是必需的。 同一应用程序清单`dependency`中可能有多个实例。

 `dependency`元素没有属性，并且包含以下子元素。

### <a name="dependentos"></a>dependentOS
 可选。 `osVersionInfo`包含元素。 和元素互相排斥：一个`dependency`元素必须存在，而不能同时存在。 `dependentAssembly` `dependentOS`

 `dependentOS`支持下列特性。

|特性|描述|
|---------------|-----------------|
|`supportUrl`|可选。 指定依赖平台的支持 URL。 如果找到所需平台，则向用户显示此 URL。|
|`description`|可选。 以用户可读的形式描述`dependentOS`元素描述的操作系统。|

### <a name="osversioninfo"></a>osVersionInfo
 必需。 此元素是 `dependentOS` 元素的子元素，并且包含 `os` 元素。 此元素没有属性。

### <a name="os"></a>操作系统
 必需。 此元素是 `osVersionInfo` 元素的子元素。 此元素具有以下属性。

|特性|描述|
|---------------|-----------------|
|`majorVersion`|必需。 指定操作系统的主版本号。|
|`minorVersion`|必需。 指定操作系统的次版本号。|
|`buildNumber`|必需。 指定 OS 的内部版本号。|
|`servicePackMajor`|必需。 指定 OS 的 Service Pack 主版本号。|
|`servicePackMinor`|可选。 指定 OS 的 Service Pack 次版本号。|
|`productType`|可选。 标识产品类型值。 有效值为 `server`、`workstation` 和 `domainController`。 例如，对于 Windows 2000 Professional，此属性值为`workstation`。|
|`suiteType`|可选。 标识系统上可用的产品套件或系统的配置类型。 有效值为 `backoffice`、`blade`、`datacenter`、`enterprise`、`home`、`professional`、`smallbusiness`、`smallbusinessRestricted` 和 `terminal`。 例如，对于 Windows 2000 Professional，此属性值为`professional`。|

### <a name="dependentassembly"></a>dependentAssembly
 可选。 `assemblyIdentity`包含元素。 和元素互相排斥：一个`dependency`元素必须存在，而不能同时存在。 `dependentAssembly` `dependentOS`

 `dependentAssembly`具有以下属性。

| 特性 | 描述 |
|-----------------------| - |
| `dependencyType` | 必需。 指定依赖项类型。 有效值为 `preprequisite` 和 `install`。 程序集作为[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序的一部分进行安装。 `install` 程序集必须存在于全局程序集缓存（GAC）中， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]然后才能安装应用程序。 `prerequisite` |
| `allowDelayedBinding` | 必需。 指定是否可以在运行时以编程方式加载程序集。 |
| `group` | 可选。 如果特性设置为`install`，则指定仅按需安装的程序集的命名组。 `dependencyType` 有关详细信息，请参见[演练：在设计器中使用 ClickOnce 部署 API 按需下载程序集](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)。<br /><br /> 如果设置为`framework` ， `dependencyType`并且属性设置为`prerequisite`，则将程序集指定为 .NET Framework 的一部分。 在 .NET Framework 4 及更高版本上安装时，不会为此程序集检查全局 assembly 缓存（GAC）。 |
| `codeBase` | 当特性设置`dependencyType`为`install`时是必需的。 依赖程序集的路径。 可以是绝对路径，也可以是相对于清单代码库的路径。 此路径必须是有效的 URI，程序集清单才有效。 |
| `size` | 当特性设置`dependencyType`为`install`时是必需的。 依赖程序集的大小（以字节为单位）。 |

### <a name="assemblyidentity"></a>assemblyIdentity
 必需。 此元素是 `dependentAssembly` 元素的子元素，并且包含下列元素。

|特性|描述|
|---------------|-----------------|
|`name`|必需。 标识应用程序的名称。|
|`version`|必需。 按以下格式指定应用程序的版本号：`major.minor.build.revision`|
|`publicKeyToken`|可选。 指定16个字符的十六进制字符串，该字符串表示用于对应用程序`SHA-1`或程序集进行签名的公钥的哈希值的最后8个字节。 用于对目录签名的公钥必须是2048位或更高。|
|`processorArchitecture`|可选。 指定处理器。 有效值`x86`适用于32位 windows 和`I64` 64 位 windows。|
|`language`|可选。 标识程序集的两部分语言代码，例如 EN-US。|

### <a name="hash"></a>hash
 元素是`assemblyIdentity`元素的可选子元素。 `hash` `hash` 元素没有属性。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]使用应用程序中所有文件的算法哈希作为安全检查，以确保在部署后没有任何文件发生更改。 如果不包含该元素，则不会执行此检查。`hash` 因此，不建议`hash`省略元素。

### <a name="dsigtransforms"></a>dsig:Transforms
 元素是`hash`元素的必需子元素。 `dsig:Transforms` `dsig:Transforms` 元素没有属性。

### <a name="dsigtransform"></a>dsig:Transform
 元素是`dsig:Transforms`元素的必需子元素。 `dsig:Transform` `dsig:Transform` 元素具有以下属性。

| 特性 | 描述 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 目前使用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]的唯一值是`urn:schemas-microsoft-com:HashTransforms.Identity`。 |

### <a name="dsigdigestmethod"></a>dsig:DigestMethod
 元素是`hash`元素的必需子元素。 `dsig:DigestMethod` `dsig:DigestMethod` 元素具有以下属性。

| 特性 | 描述 |
|-------------| - |
| `Algorithm` | 用于计算此文件摘要的算法。 目前使用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]的唯一值是`http://www.w3.org/2000/09/xmldsig#sha1`。 |

### <a name="dsigdigestvalue"></a>dsig:DigestValue
 元素是`hash`元素的必需子元素。 `dsig:DigestValue` `dsig:DigestValue` 元素没有属性。 它的文本值为指定文件的计算所得的哈希值。

## <a name="remarks"></a>备注
 应用程序使用的所有程序集都必须具有`dependency`相应的元素。 依赖程序集不包括必须在全局程序集缓存中预安装为平台程序集的程序集。

## <a name="example"></a>示例
 下面的代码示例演示`dependency`应用程序清单[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]中的元素。 此代码示例是为[ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)主题提供的更大示例的一部分。

```xml
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
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
- [\<依赖项 > 元素](../deployment/dependency-element-clickonce-deployment.md)