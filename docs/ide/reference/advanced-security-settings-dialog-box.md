---
title: “高级安全设置”对话框
ms.date: 06/27/2018
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- vs.err.debug_in_zone_no_hostproc
helpviewer_keywords:
- Advanced Security Settings dialog box
ms.assetid: 2e7aefe9-6d20-4f3e-b257-aee1ebcc6f5d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1fcc3d09e43fc5358cbe507c5045c16cc9f8cf9
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461864"
---
# <a name="advanced-security-settings-dialog-box"></a>“高级安全设置”对话框

可通过此对话框指定在区域中进行调试涉及的安全设置。

![Visual Studio 中的“高级安全设置”对话框](../media/advanced-security-settings.png)

若要访问此对话框，请在“解决方案资源管理器”  中选择项目节点，然后在“项目”  菜单上单击“属性”  。 显示“项目设计器”时，单击“安全性”选项卡   。在“安全”页上，选择“启用 ClickOnce 安全设置”，单击“这是部分可信的应用程序”，然后单击“高级”     。

## <a name="uielement-list"></a>UIElement 列表

授予应用程序对其源站点的访问权 

如果选中此复选框，应用程序可以访问发布该应用程序的网站或服务器共享。 默认情况下，该选项是选中的。

调试此应用程序，就如同它是从以下 URL 位置下载的一样 

如果需要允许应用程序访问在“发布”页上指定的“安装 URL”所对应的网站或服务器共享，请在此输入该 URL   。 此选项仅在选中“授予应用程序对其源站点的访问权限”时可用  。

## <a name="see-also"></a>请参阅

- [“项目设计器”->“安全”页](../../ide/reference/security-page-project-designer.md)