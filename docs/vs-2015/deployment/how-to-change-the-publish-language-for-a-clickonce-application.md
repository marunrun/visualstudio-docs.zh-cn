---
title: 如何：更改 ClickOnce 应用程序的发布语言 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish language property
- ClickOnce deployment, changing publish language
- publishing, ClickOnce
ms.assetid: ef5024c4-cda1-4970-bc75-32a2a10c92c3
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 26e4074b731dad44cd9eed40f1c1cc755d786562
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683800"
---
# <a name="how-to-change-the-publish-language-for-a-clickonce-application"></a>如何：更改 ClickOnce 应用程序的发布语言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在发布 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序时，在安装过程中显示的用户界面默认为开发计算机的语言和区域性。 如果要发布本地化的应用程序，则需要指定与本地化版本匹配的语言和区域性。 这取决于你的 `Publish language` 项目的属性。  
  
 `Publish language`可以在 "**发布选项**" 对话框中设置属性，该对话框可从 "**项目设计器**" 的 "**发布**" 页访问。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-change-the-publish-language"></a>更改发布语言  
  
1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。  
  
2. 单击 **“发布”** 选项卡。  
  
3. 单击 " **选项** " 按钮打开 " **发布选项** " 对话框。  
  
4. 单击 " **说明**"。  
  
5. 在 " **发布选项** " 对话框中，从 " **发布语言** " 下拉列表中选择语言和区域性，然后单击 **"确定"**。  
  
## <a name="see-also"></a>另请参阅  
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
