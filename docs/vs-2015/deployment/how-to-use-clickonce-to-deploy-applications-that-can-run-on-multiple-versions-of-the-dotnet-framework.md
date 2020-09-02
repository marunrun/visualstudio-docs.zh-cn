---
title: 如何：使用 ClickOnce 部署可在 .NET Framework 的多个版本上运行的应用程序 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65679936"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>如何：使用 ClickOnce 部署可在多个版本的 .NET Framework 上运行的应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 ClickOnce 部署技术部署面向 .NET Framework 的多个版本的应用程序。 这需要生成和更新应用程序清单和部署清单。  
  
> [!NOTE]
> 在将应用程序更改为面向 .NET Framework 的多个版本之前，应确保应用程序运行 .NET Framework 的多个版本。 版本公共语言运行时在 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 与 .NET Framework 2.0、.NET Framework 3.0 和 .NET Framework 3.5 之间有所不同。  
  
 此过程需要执行以下步骤：  
  
1. 生成应用程序和部署清单。  
  
2. 更改部署清单以列出多个 .NET Framework 版本。  
  
3. 更改 app.config 文件以列出兼容 .NET Framework 运行时版本。  
  
4. 更改应用程序清单以将依赖程序集标记为 .NET Framework 程序集。  
  
5. 对应用程序清单进行签名。  
  
6. 更新并签署部署清单。  
  
### <a name="to-generate-the-application-and-deployment-manifests"></a>生成应用程序和部署清单  
  
- 使用 "发布向导" 或 "项目设计器" 的 "发布" 页可以发布应用程序并生成应用程序和部署清单文件。 有关详细信息，请参阅 [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md) 或 [发布页、项目设计器](../ide/reference/publish-page-project-designer.md)。  
  
### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>更改部署清单以列出多个 .NET Framework 版本  
  
1. 在发布目录中，使用 Visual Studio 中的 XML 编辑器打开部署清单。 部署清单的文件扩展名为。  
  
2. 将和元素之间的 XML 代码替换为 `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` `</compatibleFrameworks>` 列出应用程序支持的 .NET Framework 版本的 xml。  
  
     下表显示了一些可用的 .NET Framework 版本和可添加到部署清单中的相应 XML。  
  
    |.NET Framework 版本|XML|  
    |----------------------------|---------|  
    |4 客户端|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|  
    |4 完整|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|  
    |3.5 客户端|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|  
    |3.5 完整|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|  
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|  
  
### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>更改 app.config 文件以列出兼容 .NET Framework 运行时版本  
  
1. 在解决方案资源管理器中，使用 Visual Studio 中的 XML 编辑器打开 App.config 文件。  
  
2. 替换 (，或在 `<startup>` `</startup>` 包含应用程序支持的 .NET Framework 运行时的 xml 的和元素之间添加) xml 代码。  
  
     下表显示了一些可用的 .NET Framework 版本和可添加到部署清单中的相应 XML。  
  
    |.NET Framework 运行时版本|XML|  
    |------------------------------------|---------|  
    |4 客户端|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|  
    |4 完整|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|  
    |3.5 完整|\<supportedRuntime version="v2.0.50727"/>|  
    |3.5 客户端|\<supportedRuntime version="v2.0.50727" sku="Client"/>|  
  
### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>更改应用程序清单以将依赖程序集标记为 .NET Framework 程序集  
  
1. 在发布目录中，使用 Visual Studio 中的 "XML 编辑器" 打开应用程序清单。 部署清单具有 .manifest 文件扩展名。  
  
2. 添加 `group="framework"` 到 sentinel 程序集的依赖项 XML (`System.Core` 、 `WindowsBase` 、 `Sentinel.v3.5Client` 和 `System.Data.Entity`) 。 例如，XML 应如下所示：  
  
    ```  
    <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">  
    ```  
  
3. 将 CommonLanguageRuntime 的元素的版本号更新 `<assemblyIdentity>` 为最小公分母的 .NET Framework 的版本号。 例如，如果应用程序以 .NET Framework 3.5 和为目标 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] ，则使用2.0.50727.0 版本号，XML 应如下所示：  
  
    ```  
    <dependency>  
      <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
        <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />  
      </dependentAssembly>  
    </dependency>  
    ```  
  
### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>更新和重新签名应用程序和部署清单  
  
- 更新并重新签署应用程序和部署清单。 有关详细信息，请参阅 [如何：对应用程序和部署清单进行重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。  
  
## <a name="see-also"></a>另请参阅  
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [\<compatibleFrameworks> Element](../deployment/compatibleframeworks-element-clickonce-deployment.md)   
 [\<dependency> Element](../deployment/dependency-element-clickonce-application.md)   
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [配置文件架构](https://msdn.microsoft.com/library/69003d39-dc8a-460c-a6be-e6d93e690b38)
