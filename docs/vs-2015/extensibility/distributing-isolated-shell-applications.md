---
title: 分发独立 Shell 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c503a985-d67a-4ef8-9123-7744a78f2f17
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bf0d8a4cab8d30a56e84d1a6869c2c842b982aea
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204665"
---
# <a name="distributing-isolated-shell-applications"></a>分发独立 Shell 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必须安装 Visual Studio 和 Visual Studio SDK，才能创建独立 shell 应用程序。 若要将应用程序分发给其他用户或客户的计算机，你必须为隔离 shell 包含一个特殊的可再发行组件包。  
  
## <a name="prerequisites-for-distributing-isolated-shell-applications"></a>分发独立 Shell 应用程序的先决条件  
  
|名称|说明|  
|----------|-----------------|  
|Visual Studio SDK|开发和测试扩展必须具有的 SDK [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 你还可以使用 SDK 创建你自己的 Visual Studio 独立 shell 的实例。<br /><br /> Visual Studio 是 SDK 的必备组件。|  
|Microsoft Visual Studio 隔离 Shell 可再发行组件|在 Visual Studio 独立 shell 上构建工具环境时，安装程序中包含的可再发行组件。 独立 Shell 可再发行组件包包括 .NET Framework 4.5。|  
  
## <a name="creating-an-installation-program-for-the-application"></a>创建应用程序的安装程序  
 必须为集成或独立 shell 应用程序创建特殊的安装程序。 有关详细信息，请参阅 [安装独立 Shell 应用程序](../extensibility/installing-an-isolated-shell-application.md)。  
  
## <a name="allowing-for-updates-to-your-application"></a>允许对应用程序进行更新  
 您的安装程序必须允许您的应用程序将通过 Microsoft 更新或您公司的更新进行更新。 有关更新的详细信息，请参阅 [独立 Shell 应用程序的服务指南](../extensibility/servicing-guidelines-for-isolated-shell-applications.md)。
