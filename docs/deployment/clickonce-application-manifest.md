---
title: ClickOnce 应用程序清单 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- application manifests [ClickOnce]
- ClickOnce, application manifests
ms.assetid: 29570cec-4e53-4660-a850-abc4fa150243
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be9bfe19b92740d6be6c91802d193bf2fc401847
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62928958"
---
# <a name="clickonce-application-manifest"></a>ClickOnce 应用程序清单
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序清单是一个 XML 文件，描述使用部署的应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单具有以下元素和属性。

| 元素 | 说明 | 属性 |
| - | - | - |
| [\<assembly> 元素](../deployment/assembly-element-clickonce-application.md) | 必需。 顶级元素。 | `manifestVersion` |
| [\<assemblyIdentity> 元素](../deployment/assemblyidentity-element-clickonce-application.md) | 必需。 标识应用程序的主要程序集 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 | `name`<br /><br /> `version`<br /><br /> `publicKeyToken`<br /><br /> `processorArchitecture`<br /><br /> `language` |
| [\<trustInfo> 元素](../deployment/trustinfo-element-clickonce-application.md) | 标识应用程序安全性要求。 | 无 |
| [\<entryPoint> 元素](../deployment/entrypoint-element-clickonce-application.md) | 必需。 标识应用程序代码入口点。 | `name` |
| [\<dependency> 元素](../deployment/dependency-element-clickonce-application.md) | 必需。 标识应用程序运行所需的每个依赖项。 （可选）标识需要进行预安装的程序集。 | 无 |
| [\<file> 元素](../deployment/file-element-clickonce-application.md) | 可选。 标识应用程序使用的每个 nonassembly 文件。 可以包括与文件关联的组件对象模型 (COM) 隔离数据。 | `name`<br /><br /> `size`<br /><br /> `group`<br /><br /> `optional`<br /><br /> `writeableType` |
| [\<fileAssociation> 元素](../deployment/fileassociation-element-clickonce-application.md) | 可选。 标识与应用程序关联的文件扩展名。 | `extension`<br /><br /> `description`<br /><br /> `progid`<br /><br /> `defaultIcon` |

## <a name="remarks"></a>备注
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序清单文件标识使用部署的应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 有关 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的详细信息，请参阅 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)。

## <a name="file-location"></a>文件位置
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序清单特定于单一版本的部署。 出于此原因，它们应与部署清单分开存储。 常见的约定是将它们放在一个子目录中，该子目录以关联版本命名。

 应用程序清单必须在部署之前进行签名。 如果手动更改应用程序清单，则必须使用 *mage.exe* 对应用程序清单进行重新签名、更新部署清单，然后对部署清单进行重新签名。 有关详细信息，请参阅 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="file-name-syntax"></a>文件名语法
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单文件的名称应为应用程序的完整名称和扩展名，如 `assemblyIdentity` 元素中所标识的那样，后跟扩展名 .manifest**。 例如，引用 *Example.exe* 应用程序的应用程序清单将使用以下文件名语法。

 `example.exe.manifest`

## <a name="example"></a>示例
 下面的代码示例演示应用程序的应用程序清单 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

```xml
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd" manifestVersion="1.0" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3" xmlns:dsig="http://www.w3.org/2000/09/xmldsig#" xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2" xmlns="urn:schemas-microsoft-com:asm.v2" xmlns:asmv1="urn:schemas-microsoft-com:asm.v1" xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">
  <asmv1:assemblyIdentity name="My Application Deployment.exe" version="1.0.0.0" publicKeyToken="43cb1e8e7a352766" language="neutral" processorArchitecture="x86" type="win32" />
  <application />
  <entryPoint>
    <assemblyIdentity name="MyApplication" version="1.0.0.0" language="neutral" processorArchitecture="x86" />
    <commandLine file="MyApplication.exe" parameters="" />
  </entryPoint>
  <trustInfo>
    <security>
      <applicationRequestMinimum>
        <PermissionSet Unrestricted="true" ID="Custom" SameSite="site" />
        <defaultAssemblyRequest permissionSetReference="Custom" />
      </applicationRequestMinimum>
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
        <!--
          UAC Manifest Options
          If you want to change the Windows User Account Control level replace the
          requestedExecutionLevel node with one of the following.

        <requestedExecutionLevel  level="asInvoker" uiAccess="false" />
        <requestedExecutionLevel  level="requireAdministrator" uiAccess="false" />
        <requestedExecutionLevel  level="highestAvailable" uiAccess="false" />

         If you want to utilize File and Registry Virtualization for backward
         compatibility then delete the requestedExecutionLevel node.
    -->
        <requestedExecutionLevel level="asInvoker" uiAccess="false" />
      </requestedPrivileges>
    </security>
  </trustInfo>
  <dependency>
    <dependentOS>
      <osVersionInfo>
        <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
      </osVersionInfo>
    </dependentOS>
  </dependency>
  <dependency>
    <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
      <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.20506.0" />
    </dependentAssembly>
  </dependency>
  <dependency>
    <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="4096">
      <assemblyIdentity name="MyApplication" version="1.0.0.0" language="neutral" processorArchitecture="x86" />
      <hash>
        <dsig:Transforms>
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
        </dsig:Transforms>
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
        <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>
      </hash>
    </dependentAssembly>
  </dependency>
<publisherIdentity name="CN=DOMAINCONTROLLER\UserMe" issuerKeyHash="18312a18a21b215ecf4cdb20f5a0e0b0dd263c08" /><Signature Id="StrongNameSignature" xmlns="http://www.w3.org/2000/09/xmldsig#">
...
</Signature></r:issuer></r:license></msrel:RelData></KeyInfo></Signature></asmv1:assembly>
```

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)