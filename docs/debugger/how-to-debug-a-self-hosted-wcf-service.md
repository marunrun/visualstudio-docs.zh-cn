---
title: 如何 - 调试自承载 WCF 服务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, self-hosted service
- WCF, debugging
ms.assetid: 288922be-ba3f-411e-af50-bba39c9529cc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8eda0f8bc6ee20a706eb74336c43d86934a9e457
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350363"
---
# <a name="how-to-debug-a-self-hosted-wcf-service"></a>如何：调试自托管 WCF 服务
“自承载服务”是指不在 IIS、WCF 服务主机或 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 开发服务器内部运行的 WCF 服务。 调试自承载 WCF 的最简单方法是配置 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，以便当你在“调试”菜单中选择“启动调试”时同时启动客户端和服务器。

 如果 WCF 服务在内部自承载，或是无法以这种方式启动的进程（如 NT 服务），则不能使用此方法。 而是可以执行以下操作之一：

- 手动将调试器附加到承载进程。 有关详细信息，请参阅[附加到运行中的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

     — 或 —

- 开始调试客户端，然后单步执行到对服务的调用。 这要求在 app.config 文件中启用调试。 有关详细信息，请参阅 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)。

### <a name="to-start-both-client-and-host-from-visual-studio"></a>从 Visual Studio 同时启动客户端和主机

1. 创建一个同时包含客户端和服务器项目的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 解决方案。

2. 配置该解决方案，以便当你在“调试”菜单上选择“启动”时，同时启动客户端和服务器进程。

   1. 在“解决方案资源管理器”中，右键单击解决方案名称。

   2. 单击“设置启动项目”。

   3. 在“解决方案 \<name> 属性”对话框中选择“多启动项目” 。

   4. 在“多启动项目”网格中，在对应于服务器项目的行上，单击“操作”，然后选择“启动”。

   5. 在对应于客户端项目的行上，单击“操作”，然后选择“启动”。

   6. 单击 **“确定”** 。

## <a name="see-also"></a>请参阅
- [调试 WCF 服务](../debugger/debugging-wcf-services.md)
- [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)
- [如何：单步执行 WCF 服务](../debugger/how-to-step-into-wcf-services.md)