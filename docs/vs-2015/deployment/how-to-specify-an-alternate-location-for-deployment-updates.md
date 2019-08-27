---
title: 如何：指定部署更新的备用位置 |Microsoft Docs
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
ms.openlocfilehash: 9040c55b2298d18d1c87e652f76950f771bd14f5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437654"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>如何：指定部署更新的其他位置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以安装你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]最初从 CD 或文件共享，应用程序，但应用程序必须检查在 Web 上找到的定期更新。 可以部署清单中指定更新的备用位置，以便你的应用程序在初始安装后可从 Web 自行更新。  
  
> [!NOTE]
> 必须配置您的应用程序以进行本地安装使用此功能。 有关详细信息，请参见[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 此外，如果在安装[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序从网络设置的原因的备用位置[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]用于该位置进行初始安装和所有后续更新。 如果你安装本地应用程序 （例如，从 CD)，请使用原始介质执行初始安装和所有后续更新都将使用备用位置。  
  
### <a name="specifying-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>使用 MageUI.exe （基于 Windows 窗体的实用程序） 指定更新备用的位置  
  
1. 打开.NET Framework 命令提示符并键入：  
  
     **MageUI.exe**  
  
2. 上**文件**菜单中，选择**打开**以打开应用程序的部署清单。  
  
3. 选择“部署选项”选项卡  。  
  
4. 在文本框中名为**启动位置**，输入将包含应用程序更新的部署清单的目录的 URL。  
  
5. 保存部署清单。  
  
### <a name="specifying-an-alternate-location-for-updates-by-using-mageexe"></a>使用 Mage.exe 指定更新的备用位置  
  
1. 打开.NET Framework 命令提示符。  
  
2. 设置使用以下命令更新位置。 在此示例中， **HelloWorld.exe.application**是路径你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]始终具有.application 扩展名，应用程序清单和 **http://adatum.com/Update/Path** 是该的URL[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]将检查应用程序更新。  
  
     Mage -Update HelloWorld.exe.application -ProviderUrl http://adatum.com/Update/Path   
  
3. 保存该文件。  
  
    > [!NOTE]
    > 现在需要使用 Mage.exe 文件重新进行签名。 有关详细信息，请参见[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 如果从脱机媒体 CD，如安装应用程序并在计算机处于联机状态，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]首先检查由指定的 URL`<deploymentProvider>`部署清单，以确定是否更新位置包含的最新版本中的标记应用程序。 如果是这样，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]从初始安装目录中，而不是安装应用程序直接从那里，并且公共语言运行时 (CLR) 确定应用程序的信任级别使用`<deploymentProvider>`。 如果计算机处于脱机状态，或`<deploymentProvider>`无法访问，[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]从 CD、 和 CLR 安装授予信任取决于安装点; 对于 CD 安装，这意味着你的应用程序接收完全信任。 所有后续更新都将继承该信任级别。  
  
 所有[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]使用的应用程序`<deploymentProvider>`应显式声明在其应用程序清单中，所需的权限，以便应用程序不会接收的不同的计算机上的信任级别不同。  
  
## <a name="see-also"></a>请参阅  
 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)   
 [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
