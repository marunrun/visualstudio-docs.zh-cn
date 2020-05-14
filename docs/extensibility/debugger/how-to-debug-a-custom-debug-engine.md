---
title: 如何：调试自定义调试引擎 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c79790bfc9c9cd3767a453258b8c2d340f64d029
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738585"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>如何：调试自定义调试引擎
项目类型从<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A>方法启动调试引擎 （DE）。 这意味着 DE 是在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]控制项目类型的实例的控制下启动的。 但是，该[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实例无法调试 DE。 下面的步骤允许您调试自定义 DE。

> [!NOTE]
> ：在"调试自定义调试引擎"过程中，您必须等待 DE 启动，然后才能附加到它。 如果在 DE 开始时出现在 DE 开头附近放置一个消息框，则可以在此时附加，然后清除消息框以继续。 这样，您可以捕获所有 DE 事件。

> [!WARNING]
> 在尝试以下过程之前，必须安装远程调试。 有关详细信息，请参阅[远程调试](../../debugger/remote-debugging.md)。

## <a name="debug-a-custom-debug-engine"></a>调试自定义调试引擎

1. 启动*msvsmon.exe，* 远程调试监视器。

2. 从*msvmon.exe*中的 **"工具**"菜单中，选择 **"选项**"以打开 **"选项**"对话框。

3. 选择"无身份验证"选项，然后单击 **"确定**"。

4. 启动 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实例并打开自定义 DE 项目。

5. 启动启动 DE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的第二个实例并打开自定义项目（为了开发，这通常在安装 VSIP 时设置的实验注册表配置单元中）。

6. 在 这第二[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]个实例中，从自定义项目加载源文件，然后启动要调试的程序。 等待片刻以允许 DE 加载，或等待，直到断点被击中。

7. 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]（使用 DE 项目）的第一个实例中，从**调试**菜单中选择 **"附加到进程**"。

8. 在 **"附加到进程"** 对话框中，更改"**传输**到**远程"（仅本机，没有身份验证）。**

9. 将**限定符**更改为计算机的名称（注意：有条目的历史记录，因此只需键入此名称一次）。

10. 在 **"可用进程"** 列表中，选择正在运行的 DE 实例，然后单击"**附加"** 按钮。

11. 在 DE 中加载符号后，在 DE 代码中放置断点。

12. 每次停止并重新启动调试过程时，请重复步骤 6 到 10。

## <a name="debug-a-custom-project-type"></a>调试自定义项目类型

1. 从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]普通注册表配置单元开始并加载项目类型项目（这是项目类型的源，而不是项目类型的实例化）。

2. 打开项目属性并转到**调试**页。 对于**命令**，键入 IDE 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]路径（默认情况下，这是 *[驱动器]*[程序文件]微软[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]8_Common7_IDE_devenv.exe）。

3. 对于**命令参数**，键入`/rootsuffix exp`实验注册表配置单元（在安装 VSIP 时创建）。

4. 单击“确定” **** 接受这些更改。

5. 通过按**F5**启动项目类型。 这将启动[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的第二个实例。

6. 此时，您可以在项目类型源代码中放置断点。

7. 在 的二个[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实例中，加载或创建项目类型的新实例。 在加载或创建过程中，您的断点可能会被击中。

8. 调试项目类型。

9. 如果选择调试启动 DE 的过程，则可以执行"调试自定义调试引擎"过程中的步骤，以在启动 DE 后附加到 DE。 这为您提供了三个[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]运行实例：一个用于项目类型源，第二个用于实例化项目类型，第三个实例附加到 DE。

## <a name="see-also"></a>请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
