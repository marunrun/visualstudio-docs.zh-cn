---
title: 视觉工作室外壳 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704002"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
shell[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]是 集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的主要代理。 shell 提供必要的功能，使 VSPackages 能够共享公共服务。 由于体系结构目标是[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在 VSPackages 中赋予主要功能，因此 shell 是一个框架，用于提供基本功能并支持其组件 VSPackages 之间的交叉通信。

## <a name="shell-responsibilities"></a>壳牌职责
 shell 具有以下关键职责：

- 支持（通过 COM 接口）用户界面 （UI） 的基本元素。 其中包括默认菜单和工具栏、文档窗口框架或多文档接口 （MDI） 子窗口，以及工具窗口框架和停靠支持。

- 在正在运行的文档表 （RDT） 中维护所有当前打开的文档的运行列表，以便协调文档的持久性，并保证不能以多种方式或不兼容的方式打开一个文档。

- 支持命令路由和命令处理接口。 `IOleCommandTarget`

- 在适当时间加载 VS 包。 为了改进外壳的性能，必须延迟加载 VSPackage。

- 管理某些共享服务，如<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>提供基本 shell 功能，以及<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>提供基本窗口功能。

- 管理解决方案 （.sln） 文件。 解决方案包含相关项目组，类似于 Visual C++ 6.0 中的工作区 （.dsw） 文件。

- 跟踪壳范围的选择、上下文和货币。 shell 跟踪以下类型的项：

  - 当前项目

  - 当前项目项或当前项目 ID<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - **属性**窗口或`SelectionContainer`

  - 控制命令、菜单和工具栏可见性的 UI 上下文 ID 或 CmdUIGuids

  - 当前活动元素，如活动窗口、文档和撤消管理器

  - 驱动动态帮助的用户上下文属性

  外壳还调解已安装的 VS 包和当前服务之间的通信。 它支持 shell 的核心功能，并使它们可用于 集成在 中的所有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackages。 这些核心功能包括以下项目：

- **关于**对话框和初始屏幕

- **添加新和添加现有项目**对话框

- **类视图**窗口和**对象浏览器**

- **引用**对话框

- **文档大纲**窗口

- **动态帮助**窗口

- **查找**和**替换**

- **在"新建****"菜单上打开项目和****打开文件**对话框

- **"工具"** 菜单上**的选项**对话框

- **属性**窗口

- **解决方案资源管理器**

- **任务列表**窗口

- **工具箱**

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackage](../../extensibility/internals/vspackages.md)
