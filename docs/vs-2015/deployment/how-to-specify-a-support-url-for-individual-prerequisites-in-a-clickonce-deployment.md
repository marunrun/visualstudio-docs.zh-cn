---
title: 如何：有关 ClickOnce 部署中的各个系统必备项指定一个支持 URL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- ClickOnce deployment, URLs
ms.assetid: 590742c3-a286-4160-aa75-7a441bb2207b
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1907b619bcc616c73d9b9e37af30722c02bf100e
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679971"
---
# <a name="how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment"></a>如何：有关 ClickOnce 部署中的各个系统必备项指定一个支持 URL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署可以用于多个先决条件，必须在客户端计算机上可用的测试[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]要运行应用程序。 其中包括所需的最低版本[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]，操作系统，并且必须预先安装在全局程序集缓存 (GAC) 中的任何程序集的版本。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]但是，无法安装这些必备组件的任何重试。如果找不到一项必备条件，它只是停止安装，并显示一个对话框，说明安装失败的原因。  
  
 有两种方法来安装系统必备组件。 可以使用引导程序应用程序进行安装。 或者，可以指定各个系统必备项，如果找不到系统必备组件对话框的上向用户显示的支持 URL。 该 URL 引用的页面可以包含用于安装必备组件的说明的链接。 如果应用程序未指定一个单独的必备组件，一个支持 URL[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]显示作为一个整体应用程序的部署清单中指定的支持 URL，如果已定义。  
  
 虽然[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，Mage.exe 和 MageUI.exe 都可用来生成[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署，这些工具不直接支持指定各个系统必备项的支持 URL。 本文档介绍如何修改部署的应用程序清单和部署清单，以包括这些支持 Url。  
  
### <a name="specifying-a-support-url-for-an-individual-prerequisite"></a>指定一个单独的必备组件的支持 URL  
  
1. 打开应用程序清单 （.manifest 文件） 你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]在文本编辑器中应用程序。  
  
2. 对于一个操作系统必备组件中，添加`supportUrl`属性为`dependentOS`元素：  
  
    ```  
     <dependency>  
        <dependentOS supportUrl="http://www.adatum.com/MyApplication/wrongOSFound.htm">  
          <osVersionInfo>  
            <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" servicePackMinor="0" />  
          </osVersionInfo>  
        </dependentOS>  
      </dependency>  
    ```  
  
3. 公共语言运行时的某个版本的先决条件，将添加`supportUrl`属性为`dependentAssembly`指定公共语言运行时依赖项的条目：  
  
    ```  
      <dependency>  
        <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/wrongClrVersionFound.htm">  
          <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.30319.0" />  
        </dependentAssembly>  
      </dependency>  
    ```  
  
4. 必须在全局程序集缓存中预安装的程序集的先决条件，将设置`supportUrl`为`dependentAssembly`元素，它指定所需的程序集：  
  
    ```  
      <dependency>  
        <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/missingSampleGACAssembly.htm">  
          <assemblyIdentity name="SampleGACAssembly" version="5.0.0.0" publicKeyToken="04529dfb5da245c5" processorArchitecture="msil" language="neutral" />  
        </dependentAssembly>  
      </dependency>  
    ```  
  
5. 可选。 对于面向.NET Framework 4 的应用程序打开部署清单 （.application 文件） 的你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]在文本编辑器中应用程序。  
  
6. 是.NET Framework 4 的先决条件，将添加`supportUrl`属性为`compatibleFrameworks`元素：  
  
    ```  
    <compatibleFrameworks  xmlns="urn:schemas-microsoft-com:clickonce.v2" supportUrl="http://adatum.com/MyApplication/CompatibleFrameworks.htm">  
      <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />  
      <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />  
    </compatibleFrameworks>  
    ```  
  
7. 手动修改应用程序清单，必须使用数字证书，请对应用程序清单重新签名，然后更新和对的部署清单重新签名。 你必须使用 Mage.exe 或 MageUI.exe SDK 工具来完成此任务中的，重新生成使用这些文件作为[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]会删除手动更改。 有关使用 Mage.exe 清单进行重新签名的详细信息，请参阅[如何：应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 如果应用程序被标记为在部分信任环境中运行时，支持 URL 不被显示在对话框中。  
  
## <a name="see-also"></a>请参阅  
 [Mage.exe（清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [\<compatibleFrameworks > 元素](../deployment/compatibleframeworks-element-clickonce-deployment.md)   
 [ClickOnce 和验证码](../deployment/clickonce-and-authenticode.md)   
 [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
