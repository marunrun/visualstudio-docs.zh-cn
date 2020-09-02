---
title: 如何：自动递增 ClickOnce 发布版本 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], incrementing publish version automatically
- Publish Version property, incrementing
- ClickOnce deployment, incrementing publish version automatically
- publishing, ClickOnce
ms.assetid: 686ab88a-6305-4914-a05b-fe269cc0ae1e
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 50faf70e8eda6ef7ab01201102540729497eb87b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683925"
---
# <a name="how-to-automatically-increment-the-clickonce-publish-version"></a>如何：自动递增 ClickOnce 发布版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

发布 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序时，更改 `Publish Version` 属性将导致应用程序作为更新发布。 默认情况下， `Revision` `Publish Version` 每次发布应用程序时，Visual Studio 都会自动递增。  
  
 您可以在 "**项目设计器**" 的 "**发布**" 页上禁用此行为。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-disable-automatically-incrementing-the-publish-version"></a>禁用自动递增发布版本  
  
1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。  
  
2. 单击 **“发布”** 选项卡。  
  
3. 在 " **发布版本** " 部分中，清除 " **自动递增每个版本的修订版本** " 复选框。  
  
## <a name="see-also"></a>另请参阅  
 [如何：设置 ClickOnce 发布版本](../deployment/how-to-set-the-clickonce-publish-version.md)   
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
