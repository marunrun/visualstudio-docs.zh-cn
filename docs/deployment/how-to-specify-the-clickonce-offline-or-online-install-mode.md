---
title: 如何-指定 ClickOnce 脱机或联机安装模式 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, specifying install mode
- install mode
- online applications
- offline applications
- ClickOnce install mode
ms.assetid: 0aee5fc1-e966-4bda-9b8f-d9997aeaa779
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dcd9eeedfdd2a4661e3744da369a6fadc11039a3
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381751"
---
# <a name="how-to-specify-the-clickonce-offline-or-online-install-mode"></a>如何：指定 ClickOnce 脱机或联机安装模式
`Install Mode` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的将确定应用程序是脱机还是联机使用。 当你选择 **"应用程序只能联机使用**" 时，用户必须具有对 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布位置（网页或文件共享）的访问权限才能运行该应用程序。 当你选择 **"该应用程序也可以脱机使用**" 时，应用程序会将条目添加到 "**开始**" 菜单和 "**添加或删除程序**" 对话框中。当应用程序未连接时，用户可以运行该应用程序。

`Install Mode`可以在 "**项目设计器**" 的 "**发布**" 页上进行设置。

> [!NOTE]
> `Install Mode`还可以使用发布向导设置。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-make-a-clickonce-application-available-online-only"></a>使 ClickOnce 应用程序仅在联机时可用

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在 "**安装模式和设置**" 区域中，单击 **"应用程序只能联机使用"** 选项按钮。

### <a name="to-make-a-clickonce-application-available-online-or-offline"></a>使 ClickOnce 应用程序可联机或脱机使用

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在 "**安装模式和设置**" 区域中，单击 "**应用程序也可以脱机使用"** 选项按钮。

     安装后，应用程序会将条目添加到 "**开始**" 菜单和 "控制面板" 的 "**添加或删除程序**"。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)