---
title: Office 解决方案安全性疑难解答
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 921bef3514b802672296dda6d680b665f1f42482
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978310"
---
# <a name="troubleshoot-office-solution-security"></a>Office 解决方案安全性疑难解答
  本主题包含用于解决在保护 Office 解决方案时可能遇到的常见问题的提示。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trusted-solutions-cannot-be-installed-from-restricted-sites"></a>不能从受限制的站点安装受信任的解决方案
 如果在 Internet Explorer 受限的站点区域中列出该网站，用户不能从 web 位置安装解决方案。 即使该解决方案使用受信任的证书进行签名，这是如此。

 部署清单的 URL 可以分为五个区域之一：

- 我的计算机

- Internet

- 本地 intranet

- 受信任的站点

- 受限制的站点

  如果已分配给受限制的站点区域中，部署清单的位置[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]不会安装该解决方案。 如果位置已知，并且可以是受信任的用户可以从受限制的站点区域中删除位置和安装该解决方案。 有关如何管理区域的信息，请参阅[配置 ClickOnce 受信任的发行者](http://go.microsoft.com/fwlink/?LinkId=94774)。

## <a name="solutions-cannot-be-installed-from-network-file-shares-or-web-locations-when-internet-explorer-enhanced-security-configuration-or-internet-explorer-7-is-installed"></a>安装 Internet Explorer 增强安全配置或 Internet Explorer 7 时，不能从网络文件共享或 web 位置安装解决方案
 Internet Explorer 增强安全配置 （安装 ieesc 时） 在 Windows Server 2003 和更高版本和 Internet Explorer 7 及更高版本，大大限制的用户浏览 Internet 的功能。 当用户尝试安装 Office 解决方案从网络文件共享或 web 位置，它们可能会收到以下错误消息："由于使用证书来签署部署清单，此应用程序中的自定义的功能无法工作*SolutionName*不受信任。 与管理员联系以获得进一步帮助。"

 使用安装 ieesc 时和 Internet Explorer 7 及更高版本，如果部署清单的 URL 进行分类在 Internet 区域中，清单必须具有来自受信任的发行者的证书，或不能安装解决方案。 未安装 ieesc 时，默认行为是提示最终用户做出信任决定。

 若要管理影响安装 ieesc 时和 Internet Explorer 7 和更高版本，确定网站和通用命名约定 (UNC) 路径您信任，并将它们添加到其中一个受信任的安全区域 （本地 intranet 或受信任的站点）。有关如何管理区域的信息，请参阅[配置 ClickOnce 受信发布方](http://go.microsoft.com/fwlink/?LinkId=94774)。

## <a name="see-also"></a>请参阅
- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
