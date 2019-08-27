---
title: 如何：调试自定义调试引擎 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b7e710cec4536a5a1327580e56c60cb23ca36f4c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436362"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>如何：调试自定义调试引擎
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

项目类型启动的调试引擎 (DE) 从<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A>方法。 这意味着，受控制的实例的启动 DE[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]控制项目类型。 但是，该实例的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]不能调试 DE。 接下来是使你能够调试自定义设备的步骤。  
  
> [!NOTE]
> :   在"调试自定义调试引擎"过程中，你必须等待 DE 来启动，然后可以将附加到它。 如果 DE 启动时显示在 DE 开始后不久将一个消息框，您可以附加在该点，然后清除消息框以继续。 这样一来，您可以捕获所有 DE 事件。  
  
> [!WARNING]
> 您必须具有远程调试安装，然后尝试以下过程。 请参阅[远程调试](../../debugger/remote-debugging.md)有关详细信息。  
  
### <a name="debugging-a-custom-debug-engine"></a>调试自定义调试引擎  
  
1. 启动 msvsmon.exe，远程调试监视器。  
  
2. 从**工具**菜单中选择 msvsmon.exe**选项**以打开**选项**对话框。  
  
3. 选择"无身份验证"选项，然后单击**确定**。  
  
4. 启动的实例[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]并打开自定义 DE 项目。  
  
5. 启动的第二个实例[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]并打开自定义项目，它启动了 DE （对于开发，这通常是在 VSIP 安装时设置的实验性注册表配置单元中）。  
  
6. 在此第二个实例中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，加载源文件从你的自定义项目并启动要调试的程序。 等待一段时间，以允许 DE 加载，或等待，直到遇到断点。  
  
7. 中的第一个实例[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]（与 DE 项目），选择**附加到进程**从**调试**菜单。  
  
8. 在中**附加到进程**对话框中，更改**传输**到**远程 （无身份验证时仅限本机）**。  
  
9. 更改**限定符**为你的计算机的名称 (注意： 还有历史记录条目，因此需要一次键入此名称)。  
  
10. 在中**可用进程**列表中，选择的实例正在运行，并单击你 DE**附加**按钮。  
  
11. 在你 DE 中已加载符号后，DE 代码中放置断点。  
  
12. 每次停止并重新启动调试的过程，重复步骤 6 至 10。  
  
### <a name="debugging-a-custom-project-type"></a>调试自定义项目类型  
  
1. 启动[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]正常注册表配置单元和负载在你的项目中，键入的项目 （这是，根据项目类型，不在项目类型的实例化的源）。  
  
2. 打开项目属性，请转到**调试**页。 有关**命令**，键入的路径[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE (默认情况下，这是 *[驱动器]* \Program Files\Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 8\Common7\IDE\devenv.exe)。  
  
3. 有关**命令参数**，类型`/rootsuffix exp`实验注册表配置单元 （VSIP 安装时创建）。  
  
4. 单击“确定”  接受这些更改。  
  
5. 按 F5 启动您的项目类型。 这将启动的第二个实例[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
6. 此时，您可以在项目类型源代码中放置断点。  
  
7. 第二个实例中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、 加载或创建您的项目类型的新实例。 在负载或创建中，可能会命中断点。  
  
8. 调试您的项目类型。  
  
9. 如果您选择要调试的启动部署过程，您可以在"调试自定义调试引擎"过程中将它启动后附加到你 DE 执行步骤。 这将使您的三个实例[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]运行： 一个用于您的项目类型源、 实例化的项目类型和第三个附加到你 DE 第二个。  
  
## <a name="see-also"></a>请参阅  
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
