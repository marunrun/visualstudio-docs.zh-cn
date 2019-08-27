---
title: PTVS 入门：在 Azure 中构建网站 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 3bdbda36-14d2-4fde-ba42-d91042777ff6
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 61f8748a3874f32db9c235d03b6b7464bc5cecf1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62550995"
---
# <a name="getting-started-with-ptvs-building-a-website-in-azure"></a>PTVS 入门：在 Azure 中构建网站
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在 Azure 中快速构建 Python 网站。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=FJx5mutt1uk&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=6)中观看这些说明。  
  
 从“新建项目”对话框开始， 然后在 Python 项目下选择“Bottle Web 项目”。  此 [Bottle](http://bottlepy.org/docs/dev/index.html) 模板是一个基于 [Bootstrap 框架](http://getbootstrap.com/)的入门网站。  创建项目时，Visual Studio 会提示你将依赖项（本例中为 Bottle）安装到虚拟环境中。  因为要部署到 Azure 网站，所以需将依赖项添加到虚拟环境中以部署站点操作所需的位。  还需要将环境建立在32 位的 Python 2.7 或 3.4 的基础上。  创建项目后，请按 F5 开始在本地运行站点。  
  
 在 Azure 中尝试访问站点很容易。  如果没有 Azure 订阅，则可以使用 [try.azurewebsites.net](https://trywebsites.azurewebsites.net/)。  此站点提供了一个简单方法：通过社会化登录，一次课访问 Azure 网站一小时。  不需要信用卡。  在“更改语言”下拉列表中选择“空站点”模板并选择“创建”。  在“使用 Web 应用程序”下，选择“下载发布配置文件”，并保存文件以供 Visual Studio 使用。  还可以使用任何操作系统中的 git 进行部署。  
  
 切换回 Visual Studio 和所创建的项目。  在“解决方案资源管理器”中选择你的项目节点，然后依次选择“右指针按钮”和“发布”。  如果你有 Azure 订阅，可以在对话框中单击“Microsoft Azure 网站”以从此处管理你的站点。  对于本演练，请选择“导入”以导入刚下载的发布配置文件。  由于发布配置文件具有所有必需的信息，因此你可以选择“发布”。  在几秒钟内将打开一个新的浏览器窗口，并且你的站点将实时承载在 Azure 云上。  
  
 简单的网站很容易，但有关 Azure 中更重要的 Web 应用程序的信息，请参阅[深入了解](https://www.youtube.com/watch?v=WG3pGmoo8nE&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=10)视频以及此通道（入门或深入了解视频页面右上角以及下方的链接）中的其他内容。  
  
 你可以在很短的 [youtube 视频](https://www.youtube.com/watch?v=FJx5mutt1uk&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=6)中观看这些说明。  
  
## <a name="see-also"></a>请参阅  
 [Wiki 文档](https://github.com/Microsoft/PTVS/wiki/Web-Project)   
 [PTVS 入门和深入了解视频](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
