---
title: 选择 ClickOnce 更新策略 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- application updates, ClickOnce
- updates, ClickOnce
- ClickOnce deployment, update strategies
ms.assetid: d8b6e7bb-4ea0-47f3-91cd-48580bdceccc
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8215b8e0955b79224341d5d43b51a473740f5fe5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442340"
---
# <a name="choosing-a-clickonce-update-strategy"></a>选择 ClickOnce 更新策略
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 可以提供应用程序自动更新。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序会定期读取其部署清单文件，以查看是否有可用的应用程序更新。 如果有，则会下载并运行应用程序的新版本。 为提高效率，仅下载那些已更改的文件。  
  
 设计 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序时，需要确定应用程序将使用何种策略来检查可用的更新。 有三种基本策略可以使用：在应用程序启动时检查更新、在应用程序启动后检查更新（在后台线程中运行）或是提供进行更新的用户界面。  
  
 此外，还可以确定应用程序检查更新的时间间隔，并且可以强制必须执行更新。  
  
> [!NOTE]
> 应用程序更新需要网络连接。 如果不存在网络连接，则应用程序会在不检查更新的情况下运行，而无论选择的是何种更新策略。  
  
> [!NOTE]
> 在 .NET Framework 2.0 和 .NET Framework 3.0 中，任何时候应用程序检查更新（无论在启动应用程序之前、之后，还是使用 <xref:System.Deployment.Application> API 时），都必须在部署清单中设置 `deploymentProvider`。 `deploymentProvider` 元素对应于 Visual Studio 中“发布”选项卡的“更新”对话框上的“更新位置”字段。在 .NET Framework 3.5 中，此规则为宽松规则。 有关详细信息，请参阅[部署 ClickOnce 应用程序的测试和生产服务器，而无需 Resigning](../deployment/deploying-clickonce-applications-for-testing-and-production-servers-without-resigning.md)。  
  
## <a name="checking-for-updates-after-application-startup"></a>在应用程序启动后检查是否有更新  
 通过使用此策略，应用程序会在运行期间尝试在后台查找并读取部署清单文件。 如果有某个更新可用，则当用户下一次运行应用程序时，会提示用户下载并安装该更新。  
  
 此策略最适用于低带宽的网络连接或可能需要长时间下载的较大应用程序。  
  
 若要启用此更新策略，请在“应用程序更新”对话框的“选择应用程序何时应该检查更新”部分中单击“在应用程序启动后”。 然后在“指定应用程序检查更新的频率”部分中指定一个更新时间间隔。  
  
 这种方式的效果与下面更改部署清单中“Update”元素的效果相同：  
  
```  
<!-- When to check for updates -->  
<subscription>  
   <update>  
      <expiration maximumAge="6" unit="hours" />  
   </update>  
</subscription>  
```  
  
## <a name="checking-for-updates-before-application-startup"></a>在应用程序启动前检查是否有更新  
 默认策略是在应用程序启动前尝试查找并读取部署清单文件。 通过使用此策略，每当用户启动应用程序时，应用程序都会尝试查找并读取部署清单文件。 如果有某个更新可用，则会下载并启动该更新；否则，会启动现有版本的应用程序。  
  
 此策略最适用于高带宽的网络连接；在低带宽连接上启动应用程序时的长时间延迟可能令人无法接受。  
  
 若要启用此更新策略，请在“应用程序更新”对话框的“选择应用程序何时应该检查更新”部分中单击“在应用程序启动前”。  
  
 这种方式的效果与下面更改部署清单中“Update”元素的效果相同：  
  
```  
<!-- When to check for updates -->  
<subscription>  
   <update>  
      <beforeApplicationStartup />  
   </update>  
</subscription>  
```  
  
## <a name="making-updates-required"></a>强制执行更新  
 在有些情况下，您可能需要要求用户运行更新版本的应用程序。 例如，你可能对诸如 Web 服务等外部资源进行了某种更改，而这种更改会使得较早版本的应用程序不能正常工作。 在这种情况下，您需要将更新标记为“必需”，并阻止用户运行较早的版本。  
  
> [!NOTE]
> 虽然使用其他更新策略也可以强制进行更新，但是“在应用程序启动前”进行检查是保证不运行较早版本的应用程序的唯一方法。 如果在启动时检测到强制更新，则用户必须要么接受更新，要么关闭应用程序。  
  
 若要将更新标记为“必需”，请单击“应用程序更新”对话框中的“指定该应用程序需要的最低版本”，然后指定发布版本（“主版本”、“次版本”、“内部版本”、“修订版本”），该发布版本指定可以安装的应用程序的最低版本号。  
  
 这种方式的效果与设置部署清单中“Deployment”元素的“minimumRequiredVersion”属性的效果相同；例如：  
  
```  
<deployment install="true" minimumRequiredVersion="1.0.0.0">  
```  
  
## <a name="specifying-update-intervals"></a>指定更新时间间隔  
 还可以指定应用程序检查更新的频率。 若要执行此操作，请指定应用程序在启动后检查是否有更新，如本主题前面的“在应用程序启动后检查是否有更新”中所述。  
  
 若要指定更新时间间隔，请在“应用程序更新”对话框中设置“指定应用程序检查更新的频率”属性。  
  
 这种方式的效果与设置部署清单中“Update”元素的“maximumAge”和“unit”属性的效果相同。  
  
 例如，您可能希望在应用程序每次运行时都进行检查，或是一周检查一次，或一个月检查一次。 如果在指定时间不存在网络连接，则更新检查会在应用程序下一次运行时执行。  
  
## <a name="providing-a-user-interface-for-updates"></a>提供进行更新的用户界面  
 在使用此策略时，应用程序开发人员会提供一个用户界面，用户可通过该用户界面选择应用程序检查更新的时间或频率。 例如，可以提供一个“立即检查更新”命令，或是一个提供有不同更新时间间隔选项的“更新设置”对话框。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署 API 提供了一个框架，此框架用于对自己的更新用户界面进行编程。 有关更多信息，请参见 <xref:System.Deployment.Application> 命名空间。  
  
 如果应用程序使用部署 API 控制它自己的更新逻辑，则应按以下部分在“阻止更新检查”中介绍的那样阻止更新检查。  
  
 此策略最适用于您需要为不同用户提供不同更新策略的情况。  
  
## <a name="blocking-update-checking"></a>阻止更新检查  
 还可以阻止应用程序检查更新。 例如，您可能有一个永不更新的简单应用程序，但您希望利用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署所提供的安装便利。  
  
 如果应用程序使用部署 API 执行它自己的更新，也应阻止更新检查；请参见本主题前面的“提供进行更新的用户界面”。  
  
 若要阻止更新检查，请清除“应用程序更新”对话框中的“应用程序应该检查更新”复选框。  
  
 也可以通过从部署清单中移除 `<Subscription>` 标记来阻止更新检查。  
  
## <a name="permission-elevation-and-updates"></a>权限提升和更新  
 如果新版本的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序需要比以前版本高的信任级别才能运行，则 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 会提示用户，询问其是否希望向该应用程序授予此较高的信任级别。 如果用户拒绝授予较高的信任级别，则将不安装更新。 下次重启该应用程序时，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 会再次提示用户安装该应用程序。 如果用户此时拒绝授予较高的信任级别，并且更新并未标记为“必需”，则该应用程序的早期版本将会运行。 但是，如果更新是“必需”的，则在用户接受较高的信任级别之前，该应用程序不会再次运行。  
  
 如果使用受信任的应用程序部署，则不会出现任何信任级别提示。 有关详细信息，请参阅 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Deployment.Application>   
 [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)   
 [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)   
 [ClickOnce 如何执行应用程序更新](../deployment/how-clickonce-performs-application-updates.md)   
 [如何：管理 ClickOnce 应用程序的更新](../deployment/how-to-manage-updates-for-a-clickonce-application.md)
