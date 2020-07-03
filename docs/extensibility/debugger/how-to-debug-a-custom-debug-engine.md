---
title: 如何：调试自定义调试引擎 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a65e69655c4e8699bd267f1835ec0c49603014d7
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903302"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>如何：调试自定义调试引擎
项目类型从方法启动调试引擎（DE） <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> 。 这意味着在控制项目类型的实例的控制下启动 DE [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 但是，此实例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 无法调试 DE。 下面是允许您调试自定义 DE 的步骤。

> [!NOTE]
> ：在 "调试自定义调试引擎" 过程中，您必须等待该操作启动后才能附加到它。 如果在开始时显示的 "de" 开头附近放置一个消息框，则可以在该点附加该消息框，然后清除该消息框以继续。 这样一来，您就可以捕获所有的消除事件。

> [!WARNING]
> 在尝试以下过程之前，必须先安装远程调试。 有关详细信息，请参阅[远程调试](../../debugger/remote-debugging.md)。

## <a name="debug-a-custom-debug-engine"></a>调试自定义调试引擎

1. 启动*msvsmon.exe*远程调试监视器。

2. 从*msvsmon.exe*中的 "**工具**" 菜单中，选择 "**选项**" 以打开 "**选项**" 对话框。

3. 选择 "无身份验证" 选项，然后单击 **"确定**"。

4. 启动实例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，并打开自定义 DE 项目。

5. 启动的第二个实例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，并打开用于启动 "DE" 的自定义项目（对于开发，这通常在安装 VSIP 时设置的实验性注册表配置单元中）。

6. 在的第二个实例中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，从自定义项目加载源文件，并启动要调试的程序。 请稍等片刻以允许取消加载，或等待，直到命中断点。

7. 在第一个实例中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] （对于 DE 项目），从 "**调试**" 菜单中选择 "**附加到进程**"。

8. 在 "**附加到进程**" 对话框中，将**传输**更改为 "**远程" （仅限本机，不进行身份验证）**。

9. 将**限定符**更改为你的计算机的名称（注意：存在条目历史记录，因此你只需键入此名称一次）。

10. 在 "**可用进程**" 列表中，选择正在运行的正在运行的实例，然后单击 "**附加**" 按钮。

11. 在您的 DE 中加载符号后，在您的 DE 代码中放置断点。

12. 每次停止并重新启动调试进程时，请重复步骤6到步骤10。

## <a name="debug-a-custom-project-type"></a>调试自定义项目类型

1. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在正常的注册表配置单元中启动并加载项目类型项目（这是项目类型的源，而不是项目类型的实例化）。

2. 打开项目属性，并中转到 "**调试**" 页。 对于**命令**，键入 IDE 的路径 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] （默认情况下为 *[drive]* \Program Files\Microsoft [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 8\Common7\IDE\devenv.exe）。

3. 对于**命令参数**，请 `/rootsuffix exp` 为试验性注册表配置单元键入（在安装 VSIP 时创建）。

4. 单击“确定” **** 接受这些更改。

5. 按**F5**启动项目类型。 这会启动的第二个实例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

6. 此时，可以将断点放置在项目类型源代码中。

7. 在的第二个实例中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，加载或创建项目类型的新实例。 在加载或创建过程中，可能会命中断点。

8. 调试项目类型。

9. 如果选择调试启动 DE 的过程，则可以执行 "调试自定义调试引擎" 过程中的步骤，以便在启动后将其附加到您的 DE。 这将提供三个 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 运行实例：一个用于项目类型源，另一个用于实例化项目类型，第三个实例附加到你的 DE。

## <a name="see-also"></a>另请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
