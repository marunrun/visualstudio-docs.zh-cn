---
title: Visual Studio Shell |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 60aa48da701857508f9b6fd7fc3d9d0c0603046e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722056"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
@No__t_0 shell 是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中集成的主代理。 Shell 提供使 Vspackage 共享公共服务所需的功能。 由于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的体系结构目标是在 Vspackage 中背心主要功能，因此外壳是一个框架，用于提供基本功能，并支持其组件 Vspackage 间的跨通信。

## <a name="shell-responsibilities"></a>Shell 责任
 Shell 具有以下关键职责：

- 支持（通过 COM 接口）用户界面（UI）的基本元素。 其中包括默认菜单和工具栏、文档窗口框架或多文档界面（MDI）子窗口和工具窗口框架，以及停靠支持。

- 在正在运行的文档表（RDT）中维护所有当前打开的文档的运行列表，以便协调文档的持久性，并确保一个文档不能以多种方式打开或以不兼容的方式打开。

- @No__t_0 支持命令路由和命令处理接口。

- 在适当的时间加载 Vspackage。 延迟加载 VSPackage 是改进 shell 性能的必需项。

- 管理某些共享服务，如 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> （提供基本 shell 功能）和 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> （提供基本的窗口化功能）。

- 管理解决方案（.sln）文件。 解决方案包含一组相关项目，类似于 Visual C++ 6.0 中的工作区（. dsw）文件。

- 跟踪 shell 范围选择、上下文和货币。 Shell 跟踪以下类型的项：

  - 当前项目

  - 当前项目项或 ItemID 当前的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - "**属性**" 窗口或 `SelectionContainer` 的当前选定内容

  - 控制命令、菜单和工具栏的可见性的 UI 上下文 Id 或 CmdUIGuids

  - 当前处于活动状态的元素，例如活动窗口、文档和撤消管理器

  - 驱动动态帮助的用户上下文属性

  Shell 还会在已安装的 Vspackage 与当前服务之间进行通信。 它支持 shell 的核心功能，并使它们可用于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中集成的所有 Vspackage。 这些核心功能包括以下各项：

- "**关于**" 对话框和初始屏幕

- "**添加新项" 和 "添加现有项**" 对话框

- **类视图**窗口和**对象浏览器**

- "**引用**" 对话框

- "**文档大纲**" 窗口

- **动态帮助**窗口

- **查找**和**替换**

- **打开**"**新建**" 菜单上的 "项目" 和 "**打开文件**" 对话框

- "**工具**" 菜单上的 "**选项**" 对话框

- “属性”窗口

- **解决方案资源管理器**

- **任务列表**窗口

- **工具箱**

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackage](../../extensibility/internals/vspackages.md)