---
title: 如何：调试自我托管的 WCF 服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, self-hosted service
- WCF, debugging
ms.assetid: 288922be-ba3f-411e-af50-bba39c9529cc
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e58acc6323f396f9b0755e84b369ce0fdf413c08
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185170"
---
# <a name="how-to-debug-a-self-hosted-wcf-service"></a>如何：调试自托管 WCF 服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“自承载服务”是指不在 IIS、WCF 服务主机或 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 开发服务器内部运行的 WCF 服务  。 若要调试自托管的 WCF 的最简单方法是配置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]以启动客户端和服务器选择时**启动调试**上**调试**菜单。  
  
 如果内部，或者不能以这种方式，如 NT 服务启动进程自承载 WCF 服务不能使用此方法。 相反，可以执行以下操作：  
  
- 手动将调试器附加到宿主进程。 有关详细信息，请参阅[附加到运行中的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。  
  
     — 或 —  
  
- 开始调试客户端，并随后单步执行对服务的调用。 这要求你启用调试在 app.config 文件中。 有关详细信息[WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)。  
  
### <a name="to-start-both-client-and-host-from-visual-studio"></a>若要从 Visual Studio 启动客户端和主机  
  
1. 创建[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]包含客户端和服务器项目的解决方案。  
  
2. 将解决方案配置为在你选择时启动客户端和服务器进程**启动**上**调试**菜单。  
  
    1. 在中**解决方案资源管理器**，右键单击解决方案名称。  
  
    2. 单击**设置启动项目**。  
  
    3. 在“解决方案 \<名称> 属性”对话框中选择“多启动项目”   。  
  
    4. 在中**多个启动项目**网格中的，对应于服务器项目中，在行上单击**操作**，然后选择**启动**。  
  
    5. 在与客户端项目相对应的行中，单击**操作**，然后选择**启动**。  
  
    6. 单击 **“确定”** 。  
  
## <a name="see-also"></a>请参阅  
 [调试 WCF 服务](../debugger/debugging-wcf-services.md)   
 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)   
 [如何：单步执行 WCF 服务](../debugger/how-to-step-into-wcf-services.md)
