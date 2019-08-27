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
ms.openlocfilehash: d570c181125a1f94108624e6f9b1ce23bdcca25a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63447217"
---
# <a name="shell-isolated-or-integrated"></a>Shell （独立或集成）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在集成或独立模式下，可以创建自己的基于 Visual Studio 的应用程序。 在集成模式下，许多 Visual Studio 功能可用于除你的应用程序。 在独立模式下，选择你想要分发以及自己的扩展的 Visual Studio 功能的子集。  
  
## <a name="integrated-mode"></a>集成模式下  
 集成的模式使用户能够使用标准 Visual Studio 功能，以及自定义工具。 集成的外壳主要面向托管编程语言和软件开发工具。  
  
 与任何其他版本的 Visual Studio 安装在同一台计算机上的合并会自动生成在集成外壳程序中的自定义工具。 如果尚未安装 Visual Studio，可以提供 Visual Studio 集成 shell 可再发行组件的版本。  
  
 Visual Studio 集成 shell 可再发行组件版本不包括编程语言和支持其相应项目系统的功能。  
  
> [!NOTE]
> 可以与 Visual Studio 除 Express 以外的所有版本一起安装 Visual Studio shell 集成模式。  
  
 有关详细信息，请参阅[Visual Studio Shell （集成）](../extensibility/visual-studio-shell-integrated.md)。  
  
## <a name="isolated-mode"></a>隔离的模式  
 独立的模式允许您创建自定义工具运行的同时与其他版本的 Visual Studio。 它主要适用于可以访问 Visual Studio 服务而不根据所有标准的 Visual Studio 功能的工具。 可以自定义 Visual Studio 独立 shell 基础上构建的应用程序的外观。 可以轻松地关闭功能并不希望与您的应用程序一起显示的菜单命令组。  
  
 有关详细信息，请参阅[Visual Studio 独立 Shell](../extensibility/visual-studio-isolated-shell.md)。  
  
## <a name="distributing-your-integrated-or-isolated-shell-application"></a>将集成或独立 Shell 应用程序分发  
 若要分发集成或独立 shell 应用程序，您需要以包括你的应用程序、 可再发行组件，一个特殊集成或独立 shell 和安装程序。 有关分发和安装的详细信息，请参阅[分发独立 Shell 应用程序](../extensibility/distributing-isolated-shell-applications.md)。  
  
> [!IMPORTANT]
> [最终用户许可协议 (EULA)](https://www.visualstudio.com/support/legal/mt171552)为 Visual Studio 集成和独立 shell 包括一节介绍了数据收集 (**第 3 部分。数据**)。  它介绍了从构建到你的应用程序的任一集成或独立 shell 软件的用户可能由 Microsoft 收集的客户使用情况数据。 有关详细信息，请参阅[Microsoft Visual Studio 产品系列隐私声明](https://www.visualstudio.com/dn948229)。  
> 
> 如果从客户收集单独使用情况数据，通过你的应用程序，您必须向您收集的应用程序的用户提供相应通知。  将独立或集成 shell 软件分发的应用程序中，根据 Visual Studio 软件开发工具包许可证，一部分时必须包括以下项之一：  
> 
> - 最终用户许可协议为应用程序许可证的一部分  
> - 要求在客户同意的条款来保护在 Visual Studio 自己 EULA 集成或独立 shell 至少要作为命令行程序软件的 Microsoft 最终用户许可条款  
  
## <a name="additional-resources"></a>其他资源  
 有关可再发行组件包的详细信息，请参阅[Visual Studio 扩展性下载](http://go.microsoft.com/fwlink/?LinkID=119298)Web 站点。  
  
## <a name="see-also"></a>请参阅  
 [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
