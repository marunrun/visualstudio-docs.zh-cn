---
title: Shell （独立或集成） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell
- Visual Studio, Shell
- Shell [Visual Studio]
- Visual Studio shell, shell-based applications
- Shell [Visual Studio], shell-based applications
ms.assetid: c64a9bf0-9bf8-45c3-8fa2-306fa6cab66a
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0db0ab2c2a97f7cedde5b9b3a5ab925467a25146
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300478"
---
# <a name="shell-isolated-or-integrated"></a>Shell（独立或集成）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在集成模式或隔离模式下创建自己的基于 Visual Studio 的应用程序。 在集成模式下，除应用程序外，还提供许多 Visual Studio 功能。 在隔离模式下，你可以选择想要随自己的扩展一起分发的 Visual Studio 功能的子集。  
  
## <a name="integrated-mode"></a>集成模式  
 集成模式使用户能够将标准 Visual Studio 功能与自定义工具一起使用。 集成外壳主要用于托管编程语言和软件开发工具。  
  
 在集成 shell 上构建的自定义工具会自动与安装在同一台计算机上的任何其他 Visual Studio 版本合并。 如果尚未安装 Visual studio，可以提供 Visual Studio 集成 shell 的可再发行版本。  
  
 Visual Studio 集成 shell 的可再发行版本不包括编程语言和支持各自的项目系统的功能。  
  
> [!NOTE]
> Visual Studio shell 集成模式可以与 Visual Studio 的所有版本（速成版除外）一起安装。  
  
 有关详细信息，请参阅[Visual Studio Shell （集成）](../extensibility/visual-studio-shell-integrated.md)。  
  
## <a name="isolated-mode"></a>隔离模式  
 独立模式允许创建与其他版本的 Visual Studio 并行运行的自定义工具。 它主要用于可访问 Visual Studio 服务的工具，而不取决于所有标准 Visual Studio 的功能。 你可以自定义在 Visual Studio 独立 shell 上构建的应用程序的外观。 可以轻松关闭不希望与应用程序一起显示的功能和菜单命令组。  
  
 有关详细信息，请参阅[Visual Studio 独立 Shell](../extensibility/visual-studio-isolated-shell.md)。  
  
## <a name="distributing-your-integrated-or-isolated-shell-application"></a>分发集成或独立 Shell 应用程序  
 若要分发集成或隔离 shell 应用程序，需要包含应用程序、特殊的集成或隔离 shell 可再发行组件和安装程序。 有关分发和安装的详细信息，请参阅[分发独立 Shell 应用程序](../extensibility/distributing-isolated-shell-applications.md)。  
  
> [!IMPORTANT]
> Visual Studio 集成和隔离 shell 的[最终用户许可协议（EULA）](https://www.visualstudio.com/support/legal/mt171552)包含有关数据收集的部分（第**3 部分）。数据**）。  它介绍了 Microsoft 可以从构建到应用程序的集成或隔离 shell 软件的用户收集的客户使用情况数据。 有关详细信息，请参阅[Microsoft Visual Studio 产品系列隐私声明](https://www.visualstudio.com/dn948229)。  
> 
> 如果你通过应用程序收集客户的不同使用情况数据，则你必须为你所收集的应用程序的用户提供相应的通知。  根据 Visual Studio 软件开发工具包许可证，当你将隔离或集成 shell 软件作为应用程序的一部分进行分发时，必须包括以下项之一：  
> 
> - 作为你的应用程序许可证的一部分的最终用户许可协议  
> - 你自己的 EULA，要求你的客户同意保护 Visual Studio 集成或隔离 shell 的条款至少与 shell 软件的 Microsoft 最终用户许可条款相同  
  
## <a name="additional-resources"></a>其他资源  
 有关可再发行组件包的详细信息，请参阅[Visual Studio 扩展性下载](https://go.microsoft.com/fwlink/?LinkID=119298)网站。  
  
## <a name="see-also"></a>请参阅  
 [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
