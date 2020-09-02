---
title: 本地化 ClickOnce 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- WPF, ClickOnce applications
- ClickOnce deployment, globalization
- deploying applications [ClickOnce], localizing ClickOnce applications
- localization, ClickOnce deployment
- ClickOnce deployment, download on-demand
- ClickOnce deployment, localization
- Windows Forms, ClickOnce applications
- console applications, ClickOnce applications
ms.assetid: c92b193b-054d-4923-834b-d4226a4c7a1a
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3c29bd6a58d510d98f2a08c96d0cd0bc774e197e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65680009"
---
# <a name="localizing-clickonce-applications"></a>本地化 ClickOnce 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本地化是使你的应用程序适用于特定区域性的过程。 此过程涉及使用正确的日期和货币格式、调整窗体上控件的大小以及根据需要从右到左镜像处理控件，从而将用户界面 (UI) 文本转换为特定于区域的语言。  
  
 对应用程序进行本地化将创建一个或多个附属程序集。 每个程序集均包含用户界面字符串、图像和其他特定于给定区域性的资源。 （应用程序的主可执行文件包含用于应用程序的默认区域性的字符串。）  
  
 本主题介绍为其他区域性部署 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序的三种方法：  
  
- 在单个部署中包括所有附属程序集。  
  
- 为每种区域性生成一个部署，且每个部署中均包括单个附属程序集。  
  
- 按需下载附属程序集。  
  
## <a name="including-all-satellite-assemblies-in-a-deployment"></a>在一个部署中包括所有附属程序集  
 与发布多个 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署不同，你可以发布单个包含所有附属程序集的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署。  
  
 此方法在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中为默认。 若要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中使用此方法，则无需进行任何其他工作。  
  
 若要在 MageUI.exe 中使用此方法，必须在 MageUI.exe 中将应用程序的区域性设置为 **中性** 。 接下来，必须手动将所有附属程序集包括在你的部署中。 在 MageUI.exe 中，可以通过使用应用程序清单的 "**文件**" 选项卡上的 "**填充**" 按钮添加附属程序集。  
  
 此方法的好处在于它可创建单个部署，并简化已本地化的部署。 在运行时，将根据用户 Windows 操作系统的默认区域性使用适当的附属程序集。 此方法的缺点为只要客户端计算机上安装或更新了应用程序，此方法就会下载所有附属程序集。 如果你的应用程序具有大量字符串，或客户的网络连接速度慢，则此过程在应用程序更新期间会影响性能。  
  
> [!NOTE]
> 此方法假定你的应用程序将自动调整控件的高度、宽度和位置以适应不同区域性中不同的文本字符串大小。 Windows 窗体包含各种控件和技术，这些控件和技术使你可以设计更易于本地化的窗体，其中包括 <xref:System.Windows.Forms.FlowLayoutPanel> 和 <xref:System.Windows.Forms.TableLayoutPanel> 控件以及 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。  另请参阅 [如何：使用 AutoSize 和 TableLayoutPanel 控件支持 Windows 窗体上的本地化](https://msdn.microsoft.com/library/1zkt8b33\(v=vs.110\))。  
  
## <a name="generate-one-deployment-for-each-culture"></a>为每种区域性生成一个部署  
 在此部署策略中，可以生成多个部署。 在每个部署中，仅包括特定区域性所需的附属程序集，并将该部署标记为特定于该区域性。  
  
 若要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中使用此方法，请在“发布”选项卡上将“发布语言”属性设置为所需的区域********。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将自动包括所选区域所需的附属程序集，并将排除部署中的所有其他附属程序集。  
  
 可通过在 Microsoft [!INCLUDE[winsdklong](../includes/winsdklong-md.md)] 中使用 MageUI.exe 工具实现相同的操作。 使用应用程序清单的 "**文件**" 选项卡上的 "**填充**" 按钮排除应用程序目录中的所有其他附属程序集，然后在 MageUI.exe 中的部署清单的 "**名称**" 选项卡上设置 "**区域性**" 字段。 这些步骤不仅包括正确的附属程序集，同时也将部署清单中 `assemblyIdentity` 元素上的 `language` 属性设置为相应的区域性。  
  
 发布应用程序后，必须为应用程序支持的每种其他区域性重复此步骤。 必须确保每次发布到不同的 Web 服务器目录或文件共享目录，因为每个应用程序清单将引用不同的附属程序集，并且每个部署清单将具有不同的 `language` 属性值。  
  
## <a name="downloading-satellite-assemblies-on-demand"></a>按需下载附属程序集  
 如果决定在单个部署中包括所有附属程序集，则可通过使用按需下载来提高性能，这使你能够将程序集标记为可选。 安装或更新应用程序时，将不会下载已标记的程序集。 可通过调用 <xref:System.Deployment.Application.ApplicationDeployment> 类上的 <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A> 方法，根据需要安装程序集。  
  
 按需下载附属程序集与按需下载其他类型的程序集略有不同。 有关如何使用的工具启用此方案的详细信息和代码示例 [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ，请参阅 [演练：使用 ClickOnce 部署 API 按需下载附属程序集](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)。  
  
 还可以在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中启用此方案。  另请参阅 [演练：在设计器中使用 ClickOnce 部署 API 按需下载附属程序集](https://msdn.microsoft.com/library/ms366788\(v=vs.110\)) 或 [演练：在设计器中使用 ClickOnce 部署 API 按需下载附属程序集](https://msdn.microsoft.com/library/ms366788\(v=vs.120\))。  
  
## <a name="testing-localized-clickonce-applications-before-deployment"></a>在部署前测试已本地化的 ClickOnce 应用程序  
 仅当应用程序主线程的 <xref:System.Threading.Thread.CurrentUICulture%2A> 属性设置为附属程序集的区域性时，才将附属程序集用于 Windows 窗体应用程序。 本地市场中的客户可能已经在运行 Windows 的本地化版本，并且已将区域性设置为相应默认值。  
  
 向客户提供应用程序前，你有如下三个选项，供测试已本地化的部署：  
  
- 可在 Windows 相应的本地化版本上运行自己的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。  
  
- 可在应用程序中以编程方式设置 <xref:System.Threading.Thread.CurrentUICulture%2A> 属性。 （必须在调用 <xref:System.Windows.Forms.Application.Run%2A> 方法前设置该属性。）  
  
## <a name="see-also"></a>另请参阅  
 [\<assemblyIdentity> Element](../deployment/assemblyidentity-element-clickonce-deployment.md)   
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)   
 [全球化 Windows 窗体](https://msdn.microsoft.com/library/72f6cd92-83be-45ec-aa37-9cb8e3ebc3c5)
