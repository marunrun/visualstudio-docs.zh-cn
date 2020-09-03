---
title: Visual Studio Shell |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fb89fc3b82dc7f142714608d8a669e368216c729
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704002"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]Shell 是中的集成主代理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 Shell 提供使 Vspackage 共享公共服务所需的功能。 由于的体系结构目标 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 是在 vspackage 中背心主要功能，因此 shell 是一个框架，用于提供基本功能，并支持其组件 vspackage 间的跨通信。

## <a name="shell-responsibilities"></a>Shell 责任
 Shell 具有以下关键职责：

- 支持 (通过 COM 接口) 用户界面 (UI) 的基本元素。 其中包括默认菜单和工具栏、文档窗口框架或多文档界面 (MDI) 子窗口和工具窗口框架，以及停靠支持。

- 在正在运行的文档表中维护所有当前打开的文档的运行列表 (RDT) 以便协调文档的持久性，并确保一个文档不能以多种方式打开，或者采用不兼容的方式打开。

- 支持命令路由和命令处理接口 `IOleCommandTarget` 。

- 在适当的时间加载 Vspackage。 延迟加载 VSPackage 是改进 shell 性能的必需项。

- 管理某些共享服务（例如 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> ），它提供基本的命令行功能和 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ，提供基本的窗口化功能。

-  ( .sln) 文件管理解决方案。 解决方案包含一组相关项目，类似于 ( Visual C++ 6.0) 文件中的工作区。

- 跟踪 shell 范围选择、上下文和货币。 Shell 跟踪以下类型的项：

  - 当前项目

  - 当前项目项或 ItemID 当前的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - " **属性** " 窗口的当前选定内容或 `SelectionContainer`

  - 控制命令、菜单和工具栏的可见性的 UI 上下文 Id 或 CmdUIGuids

  - 当前处于活动状态的元素，例如活动窗口、文档和撤消管理器

  - 驱动动态帮助的用户上下文属性

  Shell 还会在已安装的 Vspackage 与当前服务之间进行通信。 它支持 shell 的核心功能，并使它们可用于在中集成的所有 Vspackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 这些核心功能包括以下各项：

- "**关于**" 对话框和初始屏幕

- "**添加新项" 和 "添加现有项**" 对话框

- **类视图** 窗口和 **对象浏览器**

- "**引用**" 对话框

- "**文档大纲**" 窗口

- **动态帮助** 窗口

- **查找** 和 **替换**

- **打开**"**新建**" 菜单上的 "项目" 和 "**打开文件**" 对话框

- "**工具**" 菜单上的 "**选项**" 对话框

- **属性** 窗口

- **解决方案资源管理器**

- **任务列表** 窗口

- **工具箱**

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackages](../../extensibility/internals/vspackages.md)
