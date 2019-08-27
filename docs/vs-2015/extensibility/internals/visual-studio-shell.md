---
title: Visual Studio Shell |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ec79aab58e167ff2c935317897ba10a042a2e5a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180366"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Shell 是中的集成主代理[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 在 shell 提供了必要的功能，以允许 Vspackage 共享通用的服务。 由于体系结构的目标[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]背心在 Vspackage 中的主要功能是 shell 是一个框架，可提供基本功能并支持跨-在 Vspackage 及其组件之间进行通信。  
  
## <a name="shell-responsibilities"></a>Shell 职责  
 在 shell 具有以下主要职责：  
  
- 支持 （通过 COM 接口） 的用户界面 (UI) 的基本元素。 其中包括默认菜单和工具栏、 文档窗口框架或多文档界面 (MDI) 子窗口和工具窗口框架和停靠支持。  
  
- 维护运行文档表 (RDT) 中的所有当前打开的文档的运行列表来协调文档的持久性，并保证多个方面，或以不兼容的方式，无法打开该文档。  
  
- 支持的命令路由和命令处理的接口， `IOleCommandTarget`。  
  
- 在适当的时候加载 Vspackage。 需要改进的外壳性能延迟加载 VSPackage。  
  
- 管理某些共享服务，如<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>，它提供基本外壳程序功能和<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>，其中提供了基本窗口化功能。  
  
- 管理解决方案 (.sln) 文件。 解决方案包含的相关项目，类似于视觉对象中的工作区 (.dsw) 文件组C++6.0。  
  
- 跟踪命令行程序范围内所选内容、 上下文和货币。 Shell 跟踪以下类型的项：  
  
  - 当前项目  
  
  - 当前项目项的 ItemID 当前 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>  
  
  - 有关当前所选内容**属性**窗口或 `SelectionContainer`  
  
  - UI 上下文 Id 或 CmdUIGuids 控制命令、 菜单和工具栏的可见性  
  
  - 活动窗口、 文档和撤消管理器当前处于活动状态元素  
  
  - 驱动器动态帮助用户上下文属性  
  
  在 shell 还负责调解安装的 Vspackage 和当前服务之间的通信。 它支持 shell 的核心功能，并使所有的 Vspackage 中集成[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 这些核心功能包括以下各项：  
  
- **有关**对话框框和初始屏幕  
  
- **添加新功能和添加现有项**对话框  
  
- **类视图**窗口和**对象浏览器**  
  
- **引用**对话框  
  
- **文档大纲**窗口  
  
- **动态帮助**窗口  
  
- **查找**和**替换**  
  
- **打开项目**并**打开的文件**上的对话框**新建**菜单  
  
- **选项**对话框上的**工具**菜单  
  
- “属性”  窗口  
  
- **解决方案资源管理器**  
  
- **任务列表**窗口  
  
- **工具箱**  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>   
 [VSPackage](../../extensibility/internals/vspackages.md)
