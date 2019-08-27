---
title: 如何：使用 ClickOnce 部署可在多个版本的.NET Framework 运行的应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, multiple .NET Framework versions
- ClickOnce deployment, multiple .NET Framework versions
- deploying applications [ClickOnce], multiple .NET Framework versions
ms.assetid: e0a8c330-21bc-4eb2-b936-fd0f3c3221f1
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 164fe64f360e41c06ef3f7bfd2d8091a6ebefecd
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679936"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>如何：使用 ClickOnce 部署可在多个版本的.NET Framework 运行的应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以部署应用程序面向.NET Framework 的多个版本的使用 ClickOnce 部署技术。 这将要求您生成并更新应用程序和部署清单。  
  
> [!NOTE]
> 更改要面向的.NET framework 的多个版本的应用程序之前，应确保应用程序在运行.NET Framework 的多个版本。 版本的公共语言运行时之间的差异[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]与.NET Framework 2.0、.NET Framework 3.0 和.NET Framework 3.5。  
  
 此过程需要执行以下步骤：  
  
1. 生成应用程序和部署清单。  
  
2. 更改部署清单，若要列出多个.NET Framework 版本。  
  
3. 更改 app.config 文件，若要列出兼容.NET Framework 运行时版本。  
  
4. 更改要将标记作为.NET Framework 程序集的依赖程序集的应用程序清单。  
  
5. 对应用程序清单进行签名。  
  
6. 更新和部署清单进行签名。  
  
### <a name="to-generate-the-application-and-deployment-manifests"></a>若要生成应用程序和部署清单  
  
- 使用项目设计器的发布页或发布向导发布应用程序并生成应用程序和部署清单文件。 有关详细信息，请参阅[如何：发布 ClickOnce 应用程序使用发布向导](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)或[发布页上，项目设计器](../ide/reference/publish-page-project-designer.md)。  
  
### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>若要更改部署清单，若要列出多个.NET Framework 版本  
  
1. 在发布目录中，在 Visual Studio 中使用 XML 编辑器打开部署清单。 部署清单具有.application 文件扩展名。  
  
2. 之间的 XML 代码替换为`<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">`和`</compatibleFrameworks>`列出你的应用程序支持的.NET Framework 版本的 XML 元素。  
  
     下表显示了一些可用的.NET Framework 版本和相应的 XML 可添加到部署清单。  
  
    |.NET Framework 版本|XML|  
    |----------------------------|---------|  
    |4 客户端|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|  
    |4 完整|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|  
    |3.5 客户端|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|  
    |3.5 完整|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|  
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|  
  
### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>若要更改 app.config 文件，若要列出兼容.NET Framework 运行时版本  
  
1. 在解决方案资源管理器，通过在 Visual Studio 中使用 XML 编辑器中打开 App.config 文件。  
  
2. 替换 （或添加） 之间的 XML 代码`<startup>`和`</startup>`列出了受支持的.NET Framework 运行时为应用程序的 XML 元素。  
  
     下表显示了一些可用的.NET Framework 版本和相应的 XML 可添加到部署清单。  
  
    |.NET framework 运行时版本|XML|  
    |------------------------------------|---------|  
    |4 客户端|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|  
    |4 完整|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|  
    |3.5 完整|\<supportedRuntime version="v2.0.50727"/>|  
    |3.5 客户端|\<supportedRuntime version="v2.0.50727" sku="Client"/>|  
  
### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>若要更改要将标记作为.NET Framework 程序集的依赖程序集的应用程序清单  
  
1. 在发布目录中，在 Visual Studio 中使用 XML 编辑器打开应用程序清单。 部署清单具有.manifest 文件扩展名。  
  
2. 添加`group="framework"`sentinel 程序集的依赖项 XML 到 (`System.Core`， `WindowsBase`， `Sentinel.v3.5Client`，和`System.Data.Entity`)。 例如，XML 应如下所示：  
  
    ```  
    <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">  
    ```  
  
3. 更新的版本号`<assemblyIdentity>`Microsoft.Windows.CommonLanguageRuntime 元素到是最低通用标准.NET Framework 的版本号。 例如，如果应用程序面向.NET Framework 3.5 和[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]，使用 2.0.50727.0 版本号和 XML 应如下所示：  
  
    ```  
    <dependency>  
      <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
        <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />  
      </dependentAssembly>  
    </dependency>  
    ```  
  
### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>若要更新和重新签名的应用程序和部署清单  
  
- 更新和应用程序和部署清单重新签名。 有关详细信息，请参阅[如何：应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。  
  
## <a name="see-also"></a>请参阅  
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [\<compatibleFrameworks > 元素](../deployment/compatibleframeworks-element-clickonce-deployment.md)   
 [\<依赖项 > 元素](../deployment/dependency-element-clickonce-application.md)   
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [配置文件架构](https://msdn.microsoft.com/library/69003d39-dc8a-460c-a6be-e6d93e690b38)
