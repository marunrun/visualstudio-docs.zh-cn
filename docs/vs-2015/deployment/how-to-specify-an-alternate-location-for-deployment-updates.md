---
title: 如何：为部署更新指定备用位置 |微软文档
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- deployment update, alternative locations
ms.assetid: 7faacd35-2638-492d-80f6-6b57e5f820de
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8b6388833e6574fc1d631d391fa7b67d5f0a3372
ms.sourcegitcommit: c1339f64fbeee6f17bf80fedea81afc8dac40dc0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "82037215"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>如何：指定部署更新的其他位置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

最初可以从 CD[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]或文件共享安装应用程序，但应用程序必须检查 Web 上的定期更新。 您可以为部署清单中的更新指定备用位置，以便应用程序可以在初始安装后从 Web 进行更新。  
  
> [!NOTE]
> 必须将应用程序配置为在本地安装才能使用此功能。 有关详细信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 此外，如果从网络安装[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序，则设置备用位置会导致[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]将该位置用于初始安装和所有后续更新。 如果在本地安装应用程序（例如，从 CD），则使用原始媒体执行初始安装，并且所有后续更新都将使用备用位置。  
  
### <a name="specifying-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>使用 MageUI.exe（基于 Windows 窗体的实用程序）指定更新的备用位置  
  
1. 打开 .NET 框架命令提示符并键入：  
  
     **MageUI.exe**  
  
2. 在 **"文件**"菜单上，选择 **"打开"** 以打开应用程序的部署清单。  
  
3. 选择“部署选项”选项卡****。  
  
4. 在名为 **"启动位置"** 的文本框中，输入包含应用程序更新的部署清单的目录的 URL。  
  
5. 保存部署清单。  
  
### <a name="specifying-an-alternate-location-for-updates-by-using-mageexe"></a>使用 Mage.exe 指定更新的备用位置  
  
1. 打开 .NET 框架命令提示符。  
  
2. 使用以下命令设置更新位置。 在此示例中 **，HelloWorld.exe.应用程序**是[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序清单的路径，该清单始终具有 .应用程序扩展，并且`http://adatum.com/Update/Path`是检查应用程序更新的[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]URL。  
  
     **马age - 更新HelloWorld.exe.应用程序 -提供商\/Url http： /adatum.com/Update/Path**  
  
3. 保存文件。  
  
    > [!NOTE]
    > 现在，您需要使用 Mage.exe 重新签名文件。 有关详细信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 如果从脱机介质（如 CD）安装应用程序，并且计算机处于联机状态，请[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]首先检查部署清单中`<deploymentProvider>`标记指定的 URL，以确定更新位置是否包含应用程序的较新版本。 如果是，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]请直接从那里安装应用程序，而不是从初始安装目录安装应用程序，并且通用语言运行时 （CLR） 使用`<deploymentProvider>`确定应用程序的信任级别。 如果计算机处于脱机状态或`<deploymentProvider>`无法访问，则从 CD[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]进行安装，CLR 会根据安装点授予信任;否则，CLR 会根据安装点授予信任。对于 CD 安装，这意味着您的应用程序获得完全信任。 所有后续更新都将继承该信任级别。  
  
 使用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]`<deploymentProvider>`的所有应用程序都应在其应用程序清单中显式声明所需的权限，以便应用程序不会在不同的计算机上接收不同级别的信任。  
  
## <a name="see-also"></a>另请参阅  
 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [单击"一次性部署清单"](../deployment/clickonce-deployment-manifest.md)   
 [保护点击次数应用程序](../deployment/securing-clickonce-applications.md)   
 [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
