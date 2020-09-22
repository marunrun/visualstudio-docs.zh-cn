---
title: 命令可用性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
caps.latest.revision: 35
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f060f6c49fc02c75b3fe9f792133c9ee88c6d56c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840352"
---
# <a name="command-availability"></a>命令可用性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 上下文确定哪些命令可用。 上下文可能会更改，具体取决于当前项目、当前编辑器、已加载的 Vspackage，以及集成开发环境 (IDE) 的其他方面。  
  
## <a name="command-contexts"></a>命令上下文  
 以下命令上下文最为常见。  
  
- **IDE** IDE 提供的命令始终可用。  
  
- **VSPackage** Vspackage 可以定义要显示或隐藏命令的时间。  
  
- **项目** 仅对当前选定的项目显示项目命令。  
  
- **编辑器** 一次只能有一个编辑器处于活动状态。 活动编辑器中的命令可用。 编辑器与语言服务密切合作。 语言服务必须在关联编辑器的上下文中处理其命令。  
  
- **文件类型** 编辑器可以加载多种类型的文件。 可用命令可能会根据文件类型而变化。  
  
- **活动窗口** 最后一个活动文档窗口为键绑定 (UI) 上下文中设置用户界面。 但是，具有类似于内部 Web 浏览器的键绑定表的工具窗口还可以设置 UI 上下文。 对于多选项卡式文档窗口（如 HTML 编辑器），每个选项卡都有不同的命令上下文 GUID。 在注册工具窗口后，它将始终显示在 " **视图** " 菜单上。  
  
- **UI 上下文** UI 上下文由类的值标识 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> ，例如，在 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid> 生成解决方案时，或 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid> 调试器处于活动状态时。 多个 UI 上下文可以同时处于活动状态。  
  
## <a name="defining-custom-context-guids"></a>定义自定义上下文 Guid  
 如果尚未定义适当的命令上下文 GUID，则可在 VSPackage 中定义一个，然后根据需要对其进行编程，使其保持活动或非活动状态，以控制命令的可见性。  
  
1. 通过调用方法来注册上下文 Guid <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> 。  
  
2. 通过调用方法获取上下文 GUID 的状态 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> 。  
  
3. 通过调用方法启用和禁用上下文 Guid <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> 。  
  
    > [!CAUTION]
    > 请确保 VSPackage 不会影响任何现有的上下文 Guid，因为其他 Vspackage 可能依赖于它们。  
  
## <a name="see-also"></a>另请参阅  
 [选择上下文对象](../../extensibility/internals/selection-context-objects.md)   
 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
