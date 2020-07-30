---
title: Office 解决方案安全性疑难解答
ms.date: 02/02/2017
ms.topic: troubleshooting
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8825f1f4393d93df6a621fd71b6782c6652a9c0c
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87234804"
---
# <a name="troubleshoot-office-solution-security"></a>Office 解决方案安全性疑难解答
  本主题包含用于解决在保护 Office 解决方案时可能遇到的常见问题的提示。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trusted-solutions-cannot-be-installed-from-restricted-sites"></a>无法从受限制的站点安装受信任的解决方案
 如果网站列在 Internet Explorer 的 "受限制的站点" 区域中，则用户无法从 web 位置安装解决方案。 即使解决方案是使用受信任的证书签名的，也是如此。

 部署清单的 URL 可以分为五个区域之一：

- 我的电脑

- Internet 的虚拟网络适配器

- 本地 Intranet

- 受信任的站点

- 受限制的站点

  如果已将部署清单的位置分配给受限制的站点区域，则不 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 会安装解决方案。 如果该位置已知并且可以信任，则用户可以从受限制的站点区域中删除该位置，并安装解决方案。 有关如何管理区域的信息，请参阅[配置 ClickOnce 受信任的发布者](/previous-versions/dotnet/articles/ms996418(v=msdn.10))。

## <a name="solutions-cannot-be-installed-from-network-file-shares-or-web-locations-when-internet-explorer-enhanced-security-configuration-or-internet-explorer-7-is-installed"></a>如果安装了 Internet Explorer 增强的安全配置或 Internet Explorer 7，则无法从网络文件共享或 web 位置安装解决方案
 Internet Explorer 增强的安全配置（IEESC）在 Windows Server 2003 及更高版本以及 Internet Explorer 7 及更高版本中，大大限制了用户浏览 Internet 的能力。 当用户尝试从网络文件共享或 web 位置安装 Office 解决方案时，它们可能会收到以下错误消息： "此应用程序中的自定义功能将不起作用，因为用于对*解决方案名称*的部署清单进行签名的证书不受信任。 请与管理员联系以获得进一步的帮助。 "

 使用 IEESC 和 Internet Explorer 7 及更高版本时，如果部署清单的 URL 在 Internet 区域中分类，则清单必须具有来自受信任发布者的证书，否则无法安装解决方案。 如果没有 IEESC，则默认行为是提示最终用户做出信任决定。

 若要管理 IEESC 和 Internet Explorer 7 及更高版本的效果，请确定你信任的网站和通用命名约定（UNC）路径，并将其添加到某个受信任的安全区域（本地 intranet 或受信任的站点）。有关如何管理区域的信息，请参阅[配置 ClickOnce 受信任的发布者](/previous-versions/dotnet/articles/ms996418(v=msdn.10))。

## <a name="see-also"></a>另请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [Visual Studio 疑难解答](/troubleshoot/visualstudio/welcome-visual-studio/)
