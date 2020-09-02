---
title: “高级安全设置”对话框 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.err.debug_in_zone_no_hostproc
- vs.err.debug_in_zone_no_hostproc:11310
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Advanced Security Settings dialog box
ms.assetid: 2e7aefe9-6d20-4f3e-b257-aee1ebcc6f5d
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 000c3c4e2996869e96fd0d6097b5bab8576936a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651743"
---
# <a name="advanced-security-settings-dialog-box"></a>“高级安全设置”对话框
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可通过此对话框指定在区域中进行调试涉及的安全设置。

 若要访问此对话框，请在“解决方案资源管理器”**** 中选择项目节点，然后在“项目”**** 菜单上单击“属性”****。 当 " **项目设计器** " 出现时，单击 " **安全** " 选项卡。在 " **安全** " 页上，选择 " **启用 ClickOnce 安全设置**"，单击 " **这是部分信任的应用程序**"，然后单击 " **高级**"。

## <a name="uielement-list"></a>UIElement 列表
 **使用选定权限集调试此应用程序**如果选中此复选框，在调试期间会使用“安全”页上选中的权限集****。 默认情况下选择此选项。

 要在安全区域中进行调试必须启用此选项；此外还必须启用“启用 Visual Studio 托管进程”选项（此选项位于“项目设计器”的“调试”页上）************。

 WPF Web 浏览器应用程序项目选中并禁用了“使用选定权限集调试此应用程序”选项****。

 **授予应用程序对其源站点的访问权限**如果选中此复选框，则应用程序可以访问发布该应用程序的网站或服务器共享。 默认情况下选择此选项。

 **调试此应用程序，就如同它是从以下 URL 位置下载的一样**如果需要允许应用程序访问在“发布”页上指定的“安装 URL”所对应的网站或服务器共享，请在此键入该 URL********。 此选项仅在选中“授予应用程序对其源站点的访问权限”时可用****。

## <a name="see-also"></a>另请参阅
 [”项目设计器“ -&gt;“安全”页](../../ide/reference/security-page-project-designer.md)
