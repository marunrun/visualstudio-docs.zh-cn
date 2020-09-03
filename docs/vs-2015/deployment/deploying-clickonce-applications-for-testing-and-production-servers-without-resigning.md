---
title: 为测试服务器和生产服务器部署 ClickOnce 应用程序而不进行让步 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, deploying without resigning
- ClickOnce deployment, without resigning
- application updates, ClickOnce
- update location [ClickOnce]
- deploymentProvider tag
- manifests [ClickOnce]
ms.assetid: 1218a98d-1ad5-4eef-95dd-0e0b3c44168c
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a8e41e67d5e2800acc41e1220fe632001420a274
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80395374"
---
# <a name="deploying-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>在不重新签名的情况下为测试服务器和生产服务器部署 ClickOnce 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题讨论 .NET Framework 版本3.5 中引入的 ClickOnce 的一项新功能，该功能允许从多个网络位置部署 ClickOnce 应用程序，而无需重新签名或更改 ClickOnce 清单。  
  
> [!NOTE]
> 让步仍是部署新版本的应用程序的首选方法。 请尽可能使用让步方法。 有关详细信息，请参阅 [Mage.exe（清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)。  
  
 第三方开发人员和 Isv 可以选择启用此功能，使其客户能够更轻松地更新应用程序。 此功能可用于以下情况：  
  
- 更新应用程序时，不是第一次安装应用程序。  
  
- 当一台计算机上只有一个应用程序配置时。 例如，如果将应用程序配置为指向两个不同的数据库，则无法使用此功能。  
  
## <a name="excluding-deploymentprovider-from-deployment-manifests"></a>从部署清单中排除 deploymentProvider  
 在 .NET Framework 2.0 和 .NET Framework 3.0 中，安装在系统上以实现脱机可用性的任何 ClickOnce 应用程序都必须 `deploymentProvider` 在其部署清单中指定。 `deploymentProvider`通常称为更新位置; 它是 ClickOnce 检查应用程序更新的位置。 此要求与应用程序发布者对其部署进行签名的需求相结合，使得公司难以从供应商或其他第三方更新 ClickOnce 应用程序。 这也使得从同一网络上的多个位置部署相同的应用程序变得更加困难。  
  
 随着对 .NET Framework 3.5 中 ClickOnce 所做的更改，第三方可以向另一个组织提供 ClickOnce 应用程序，然后将该应用程序部署在其自己的网络上。  
  
 为了利用此功能，ClickOnce 应用程序的开发人员必须 `deploymentProvider` 从其部署清单中排除。 这意味着， `-providerUrl` 当你创建具有 Mage.exe 的部署清单时不包括参数，或者，如果你正在生成包含 MageUI.exe 的部署清单，请将 "**应用程序清单**" 选项卡上的 "**启动位置**" 文本框留空。  
  
## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider 和应用程序更新  
 从 .NET Framework 3.5 开始，你无需在部署清单中指定，就可以 `deploymentProvider` 部署 ClickOnce 应用程序以实现联机和脱机使用。 这就支持你需要自行打包和签名部署的方案，但允许其他公司通过其网络部署应用程序。  
  
 需要记住的要点是，排除的应用程序 `deploymentProvider` 在更新过程中无法更改其安装位置，直到它们交付包含标记的更新为止 `deploymentProvider` 。  
  
 下面是两个示例来阐明这一点。 在第一个示例中，你发布了一个没有标记的 ClickOnce 应用程序 `deploymentProvider` ，并要求用户从安装该应用程序 `http://www.adatum.com/MyApplication/` 。 如果你决定要从发布应用程序的下一个更新 `http://subdomain.adatum.com/MyApplication/` ，你将无法在驻留在中的部署清单中表示此项 `http://www.adatum.com/MyApplication/` 。 可以执行以下两项操作之一：  
  
- 告诉用户卸载以前的版本，并从新位置安装新版本。  
  
- 包括的更新 `http://www.adatum.com/MyApplication/` ，其中包含 `deploymentProvider` 指向的 `http://www.adatum.com/MyApplication/` 。 然后，稍后发布另一个更新，并 `deploymentProvider` 指向 `http://subdomain.adatum.com/MyApplication/` 。  
  
  在第二个示例中，您将发布指定的 ClickOnce 应用程序 `deploymentProvider` ，然后决定将其删除。 如果新版本未 `deploymentProvider` 下载到客户端，则在发布已还原的应用程序版本之前，你将无法重定向用于更新的路径 `deploymentProvider` 。 如第一个示例所示， `deploymentProvider` 最初必须指向当前更新位置，而不是新位置。 在这种情况下，如果尝试插入 `deploymentProvider` 引用的 `http://subdomain.adatum.com/MyApplication/` ，则下一次更新将会失败。  
  
## <a name="creating-a-deployment"></a>创建部署  
 有关创建可从不同网络位置部署的部署的分步指导，请参阅 [演练：手动部署不需要重新签名并且保留署名信息的 ClickOnce 应用程序](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required?view=vs-2015)。  
  
## <a name="see-also"></a>另请参阅  
 [Mage.exe (清单生成和编辑工具) ](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe（图形化客户端中的清单生成和编辑工具）](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)
