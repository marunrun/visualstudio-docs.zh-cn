---
title: 如何：指定 ClickOnce 应用程序的开始菜单名称 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Start menu resource name
- Start menu name
- ClickOnce deployment, Start menu name
ms.assetid: 4b5183b2-2fd4-4433-9310-4a73bb12c4e3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4ef1675480182796e1fe8bbe29baa5ed6a9d5f63
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898797"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的“开始”菜单名称
当[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序安装为联机和脱机使用，条目添加到**启动**菜单和**添加或删除程序**列表。 默认情况下，显示名称是应用程序程序集名称相同，但您可以通过设置更改显示名称**产品名称**中**发布选项**对话框。

 **产品名称**将显示在*publish.htm*页上; 对于已安装的脱机应用程序，它将中的条目的名称**启动**菜单中，并且也将在显示的名称**添加或删除程序**。

 **发布者名称**将出现*publish.htm*上述页面**产品名称**，，对于已安装的脱机应用程序，它将是包含应用程序的文件夹的名称中的图标**启动**菜单。

 在创建开始菜单快捷方式或应用程序引用 *%appdata%\Microsoft\Windows\Start Menu\Programs\\< 发布服务器名称\>*。 快捷方式或应用程序引用具有相同名称作为产品名称。

 可以设置**产品名称**并**发布服务器的名称**中的属性**发布选项**对话框中，可在上找到**发布**页**项目设计器**。

### <a name="to-specify-a-start-menu-name"></a>若要指定的开始菜单名称

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击**选项**按钮以打开**发布选项**对话框。

4. 单击**说明**。

5. 在中**发布选项**对话框框中，输入要在中显示的名称**产品名称**。

6. 或者，可以输入中的发布服务器名称**发布服务器名称**。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)