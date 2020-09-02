---
title: 受信任的应用程序部署概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- ClickOnce deployment, security
- trusted application deployment
ms.assetid: b24a1702-8fbe-45b1-87a0-9618a0708f1d
caps.latest.revision: 33
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 673cc3d9b936131e6423a015af5c78486846fbe7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75847710"
---
# <a name="trusted-application-deployment-overview"></a>Trusted Application Deployment Overview
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题概述了如何通过使用受信任的应用程序部署技术部署具有提升权限的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。  
  
 借助作为 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署技术一部分的受信任的应用程序部署，任何规模的组织都可更容易地以更安全的方式授予对托管应用程序的其他权限而无需用户提示。 通过受信任的应用程序部署，组织可以只将客户端计算机配置为具有用验证码证书标识的受信任发布者的列表。 此后，由任一这些受信任的发布者签名的任何 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序均将接收更高级别的信任。  
  
> [!NOTE]
> 受信任的应用程序部署要求一次性配置用户的计算机。 在托管的桌面环境中，可使用全局策略来执行此配置。 如果你不想对你的应用程序进行如此配置，请改用权限提升。 有关详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。  
  
## <a name="trusted-application-deployment-basics"></a>受信任的应用程序部署基础知识  
 下表显示了受信任的应用程序部署中所涉及的对象和角色。  
  
|对象或角色|说明|  
|--------------------|-----------------|  
|主要区域中的|负责更新和维护客户端计算机的组织实体|  
|信任关系管理器|公共语言运行时 (CLR) 中负责强制执行客户端应用程序安全性的的子系统。|  
|publisher|编写和维护应用程序的实体。|  
|部署人员|将应用程序打包并分发给用户的实体。|  
|证书 (certificate)|由公钥和私钥组成的加密签名；通常由可保证其可靠性的的证书颁发机构 (CA) 颁发。|  
|验证码证书|嵌入了元数据的证书，其中元数据描述证书的可能用途等信息。|  
|证书颁发机构|验证发布者身份并向其颁发内嵌发布者元数据的证书的组织。|  
|根证书颁发机构|授权其他证书颁发机构颁发证书的证书颁发机构。|  
|密钥容器|Microsoft Windows 中用于存储证书的逻辑存储空间。|  
|受信任的发布者|其验证码证书已添加到客户端计算机上的证书信任列表 (CTL) 的发布者。|  
  
 在大型组织中，发布者和部署人员通常是两个独立的实体：  
  
- 发布者是创建 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序的组。  
  
- 部署人员是将 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序分发给集团企业台式计算机的组（通常为信息技术 (IT) 部）。  
  
  必须执行以下步骤以使用受信任的应用程序部署：  
  
1. 获取发布者的证书。  
  
2. 将发布者添加到所有客户端上的受信任的发布者存储区。  
  
3. 创建你的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。  
  
4. 使用发布者的证书来签署部署清单。  
  
5. 将应用程序部署发布到客户端计算机。  
  
### <a name="obtain-a-certificate-for-the-publisher"></a>获取发布者的证书  
 数字证书是 Microsoft 验证码身份验证和安全系统的核心组件。 验证码是 Windows 操作系统的标准部分。 所有 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序均必须使用数字证书进行签名，无论它们是否参与受信任的应用程序部署。 有关验证码如何与配合使用的完整说明 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ，请参阅 [ClickOnce 和 authenticode](../deployment/clickonce-and-authenticode.md)。  
  
### <a name="add-the-publisher-to-the-trusted-publishers-store"></a>将发布者添加到受信任的发布者存储区。  
 为了你的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序能够接收更高级别的信任，必须将你的证书作为受信任的发布者添加到将运行此应用程序的每个客户端计算机。 执行此任务属于一次性的配置。 完成后，可尽可能多地随心部署用你的发布者证书进行签名的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序，且这些应用程序均将以高信任级别运行。  
  
 如果正在托管的桌面环境中部署应用程序（例如，运行 Windows 操作系统的公司 Intranet），可通过使用组策略创建新的证书信任列表 (CTL) 将受信任的发布者添加到客户端的存储区。 有关详细信息，请参阅 [为组策略对象创建证书信任列表](https://technet.microsoft.com/library/2c03582f-00b2-43e5-ae1d-493894ad0fd7)。  
  
 如果未在托管的桌面环境中部署应用程序，可使用以下选项将证书添加到受信任的发布者存储区：  
  
- <xref:System.Security.Cryptography?displayProperty=fullName> 命名空间。  
  
- CertMgr.exe，这是 Internet Explorer 的一个组件，因此存在于 Windows 98 及所有更高版本中。 有关详细信息，请参阅 [ (证书管理器工具)Certmgr.exe ](https://msdn.microsoft.com/library/7e953b43-1374-4bbc-814f-53ca1b6b52bb)。  
  
### <a name="create-a-clickonce-application"></a>创建 ClickOnce 应用程序  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序是一个结合有可描述应用程序并提供安装参数的清单文件的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 客户端应用程序。 可以使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 中的“发布” **** 命令将你的程序转换成 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]应用程序。 或者，可以使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 附带的工具生成 [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]部署所需的所有文件。 有关详细步骤[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。  
  
 受信任的应用程序部署特定于 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]且只能与 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序一起使用。  
  
### <a name="sign-the-deployment"></a>对部署进行签名  
 获取证书后，必须用它对部署进行签名。 如果正在使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 发布者向导部署应用程序，此向导将在你自身尚未指定证书时自动为你生成一个测试证书。 但是，还可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目设计器窗口提供由 CA 提供的证书。  另请参阅 [如何：使用发布向导发布 ClickOnce 应用程序](https://msdn.microsoft.com/library/31kztyey\(v=vs.110\)) 或 [如何：使用发布向导发布 ClickOnce 应用程序](https://msdn.microsoft.com/library/31kztyey\(v=vs.110\))。  
  
> [!CAUTION]
> 我们不建议使用测试证书来部署应用程序。  
  
 还可以使用 Mage.exe 或 MageUI.exe SDK 工具来签名应用程序。 有关详细信息，请参阅 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 有关与部署签名相关的命令行选项的完整列表，请参阅 [Mage.exe (清单生成和编辑工具) ](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)。  
  
### <a name="publish-the-application"></a>发布应用程序  
 一旦签名了 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 清单，应用程序即准备好发布到安装位置。 安装位置可以是 Web 服务器、文件共享或本地磁盘。 当客户端首次访问部署清单时，信任关系管理器必须选择安装的受信任发布者是否已授予 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序在更高级别的信任运行的权限。 信任关系管理器通过将用于对签名部署的证书和客户端受信任的发布者存储区中存储的证书进行比较来做出选择。 如果信任关系管理器找到匹配项，则应用程序以高信任级别运行。  
  
## <a name="trusted-application-deployment-and-permission-elevation"></a>受信任的应用程序部署和权限提升  
 如果当前发布者不是受信任的发布者，信任关系管理器将使用权限提升来询问用户是否要向你的应用程序授予提升的权限。 但是，如果管理员禁用了权限提升，则应用程序无法获取用于运行的权限。 应用程序将无法运行，并且不会向用户显示任何通知。 有关权限提升的详细信息，请参阅 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。  
  
## <a name="limitations-of-trusted-application-deployment"></a>受信任的应用程序部署的限制  
 可以使用受信任的应用程序部署通过 Web 或企业文件共享将提升的信任授予 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序。 无需对 CD 上分布的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序使用受信任的应用程序部署，因为默认情况下，以向这些应用程序授予完全信任。  
  
## <a name="see-also"></a>另请参阅  
 [Mage.exe (清单生成和编辑工具) ](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
