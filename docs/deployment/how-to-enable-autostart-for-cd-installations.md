---
title: 如何：为 CD 安装启用自动启动 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, AutoStart
- ClickOnce deployment, installation on CD or DVD
- deploying applications [ClickOnce], installation on CD or DVD
ms.assetid: caaec619-900c-4790-90e3-8c91f5347635
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66f5510ae63507aebb97a7f8bdfd3e367f1afc85
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928509"
---
# <a name="how-to-enable-autostart-for-cd-installations"></a>如何：启用 CD 安装自动启动
在部署时[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]通过可移动媒体，如 CD-ROM 或 DVD-ROM 的应用程序，可以启用`AutoStart`以便[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]插入媒体时自动启动应用程序。

 `AutoStart` 在上启用**发布**页**项目设计器**。

### <a name="to-enable-autostart"></a>若要启用自动启动

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 单击“发布”选项卡。

3. 单击“选项”按钮。

     **发布选项**对话框随即出现。

4. 单击**部署**。

5. 选择**对于 CD 安装，插入 CD 时自动启动安装程序**复选框。

     *Autorun.inf*文件将复制到发布位置，在发布应用程序。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)