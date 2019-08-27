---
title: Visual Studio 管理员指南 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
caps.latest.revision: 76
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 5a84f0a037df92ff31ce66eb6692367ef1d209f6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546653"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio Administrator Guide
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[Visual Studio 管理员指南](/visualstudio/install/visual-studio-administrator-guide)。

您可以在网络上部署 Visual Studio 2015，只要每台目标计算机满足[最低安装要求](https://visualstudio.microsoft.com/vs/older-downloads/)。 可以通过使用 /layout 开关运行安装文件（如[创建 Visual Studio 的脱机安装](../install/create-an-offline-installation-of-visual-studio.md)页所述），然后将其从本地计算机复制到网络共享来创建一个网络共享。 如果使用的 ISO，可以装载 ISO 并共享它或将 ISO 复制到网络共享。  
  
 请注意，从网络共享进行安装会“记住”它们的源位置。 这意味着客户端计算机的修复可能需要返回最初从中安装客户端的网络共享。 请仔细选择你的网络位置，使其符合在组织中运行的 Visual Studio 2015 客户端的预期生存期。  
  
## <a name="detection-and-servicing-keys"></a>检测和维护项  
 你可以使用注册表中的检测子项来确定是否已在计算机上安装 Visual Studio 产品。 你将在自动部署中使用这些检测项，以确定是否有必要继续安装。  请参阅[检测系统要求](../extensibility/internals/detecting-system-requirements.md)[检测系统要求]。  
  
## <a name="avoiding-reboots"></a>避免重新启动  
 可通过确保在部署 Visual Studio 之前满足相应的 Visual Studio 先决条件，从而减少重新启动次数。 对于.NET Framework 中，可能需要重新启动正在运行 Windows 8，如果不首先安装.NET Framework 4.6，在其上部署 Visual Studio 2015 的计算机。  
  
 对于 Windows 和 Android 设备仿真，如果尚未启用 Windows 的 HYPER-V 功能，则可能需要重新启动计算机。 对于 Web 开发，如果尚未启用 Windows 的 Web 服务器功能，则可能需要重新启动计算机。 对于 Office 开发，如果尚未启用 Windows 的 Windows Identify Foundation 功能，则可能需要重新启动计算机。 如果没有启用 Windows 的 Web 服务器功能，请重新启动计算机。 对于 Office 开发，如果尚未启用 Windows 的 Windows Identify Foundation 功能，则可能需要重新启动计算机。 若要了解有关如何自动检测和安装 Windows 功能的详细信息，请参阅 [在运行 Windows Server 2008 R2 的服务核心安装的服务器上安装服务器角色](https://technet.microsoft.com/library/ee441260(v=ws.10).aspx)。  
  
## <a name="error-return-codes"></a>错误返回代码  
 下表列出了重要的错误代码。 可以使用自动化中的这些错误代码来确定是否需要重新启动和安装是否成功。 如果收到错误代码，在考虑故障排除步骤[安装 Visual Studio](../install/install-visual-studio-2015.md)页。  
  
|安装状态|无需重启|需要重启|描述|  
|------------------|--------------------------|----------------------|-----------------|  
|成功|0x00000000 [0]|0x00000bc2 [3010]|成功安装。|  
|块|0x80044000 [-2147205120]|0x8004C000 [-2147172352]|如果唯一要报告的块是“重新启动挂起”，则返回值是“要求未完成的重新启动”值 (0x80048bc7)。|  
|取消|0x00000642 [1602]|0x80048642 [-2147187134]|返回重新启动值时，返回代码为 1602。|  
|要求未完成的重新启动|不适用|0x80048bc7 [-2147185721]|需要重新启动才能继续安装。|  
|失败|0x00000643 [1603]|0x80048643 [-2147187133]|返回重新启动值时，返回代码为 1603。|  
  
## <a name="interactive-administrator-installer"></a>交互式管理员安装程序  
 如果你正在 Visual Studio 安装程序之上创建交互式安装程序，则可以从 Visual Studio 安装程序中查看进度。 Visual Studio 2015 安装程序基于开放源代码 Windows Installer XML (WiX) 链接器技术（也称“刻录”）。 刻录技术支持两个通信协议：刻录和 netfx4。 有关简要参考，请参阅 [wixtoolset.org](http://wixtoolset.org/)处的 ExePackage 元素文档中的协议特性说明。对此协议属性的 WiX 开放源代码实现的审查可能需要进行集成。  
  
## <a name="controlling-what-is-installed"></a>控制安装的内容  
 如果要控制最终用户可以安装的内容，有两个选择：管理员文件安装和命令行选项。 如果你的目标是限制最终用户可以从其 Visual Studio 安装程序体验中所选的内容，请选择管理员文件安装。 如果要创建初始配置，但允许最终用户选择他们自己的 Visual Studio 安装程序体验，请选择命令行参数。  
  
 有关管理员文件体验的详细信息，请参阅[如何：创建并运行无人参与的安装的 Visual Studio](../install/how-to-create-and-run-an-unattended-installation-of-visual-studio.md)和[如何：部署 Visual Studio 时自动应用产品密钥](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md)。  有关命令行控件的详细信息，请参阅[使用命令行参数安装 Visual studio](../install/use-command-line-parameters-to-install-visual-studio.md)页。  
  
## <a name="specifying-customer-feedback-settings"></a>指定客户反馈设置  

默认情况下，Visual Studio 安装会启用客户反馈。 可以通过将以下注册表项的值更改为字符串 "0"，将 Visual Studio 配置为在单台计算机上禁用客户反馈：  
  
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM  
OptIn  
  
（例如，将其更改为 HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM OptIn ="0"）  
  
## <a name="related-topics"></a>相关主题  
  
|主题|描述|  
|-----------|-----------------|  
|[如何：安装特定版本的 Visual Studio](../install/how-to-install-a-specific-release-of-visual-studio.md)|介绍如何安装当前版本的特定配置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。|  
|[如何：创建和运行 Visual Studio 的无人参与安装](../install/how-to-create-and-run-an-unattended-installation-of-visual-studio.md)|介绍如何安装[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]无人参与模式。|  
|[如何：在部署 Visual Studio 时自动应用产品密钥](../install/how-to-automatically-apply-product-keys-when-deploying-visual-studio.md)|介绍如何部署到多台计算机时应用产品密钥。|  
|[帮助查看器管理员指南](../ide/help-viewer-administrator-guide.md)|提供有关如何管理本地帮助安装的或不能访问 internet 的网络环境的信息。|  
|[安装 Visual Studio](../install/install-visual-studio-2015.md)|提供相关说明和链接，这些主题介绍如何安装[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。|