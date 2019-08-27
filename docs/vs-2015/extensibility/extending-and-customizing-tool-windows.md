---
title: 扩展和自定义工具 Windows |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, essentials
- tool windows, standard
ms.assetid: 46b2892e-7b2b-4b3f-83a7-b884f1e114ee
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b232fa1275bce453e3b32cea6a5ff37fdd501c6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204547"
---
# <a name="extending-and-customizing-tool-windows"></a>扩展和自定义工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 提供多种不同类型的 windows，如工具窗口、 文档窗口和对话框窗口。 例如属性窗口、 输出窗口和任务列表窗口中，其他窗口是工具窗口的类型。  
  
## <a name="tool-windows"></a>工具窗口  
 Visual Studio 工具窗口是不基于文件的通常是只读的窗口。 在这方面，它们不同于文档窗口，文档窗口在读写模式下显示文件。 工具窗口的示例包括“工具箱”  、“解决方案资源管理器”  、“属性”  窗口和“Web 浏览器”  。  
  
 若要了解如何创建简单的工具窗口，请参阅[添加工具窗口](../extensibility/adding-a-tool-window.md)。  
  
 若要注册与 Visual Studio 工具窗口，请参阅[注册工具窗口](../extensibility/registering-a-tool-window.md)。  
  
 工具窗口默认情况下是单实例，这意味着一次只能打开一个工具窗口的实例。 打开单实例工具窗口后，它保持打开状态直到关闭 IDE。 单实例工具窗口关闭时，仅其可见性更改。 你还可以创建多实例工具窗口，以便可以同时打开窗口中的多个实例。 请参阅[创建多实例工具窗口](../extensibility/creating-a-multi-instance-tool-window.md)有关详细信息。  
  
 工具窗口可以*动态*，这意味着它们可见时应用其相关的 UI 上下文。 使用自动可见性可以减少 IDE 中的窗口的混乱。 有关详细信息，请参阅[打开动态工具窗口](../extensibility/opening-a-dynamic-tool-window.md)。  
  
 工具窗口可以在文档框架中停靠、浮动或呈选项卡式。 工具窗口框架由 IDE 提供，用于控制大小、位置、停靠状态和其他持久性属性。 工具窗口窗格用于显示内容。 仅当首次打开工具窗口时才应用默认大小和位置；在此之后将保留工具窗口状态。  
  
 工具窗口窗格可以承载 WPF 用户控件，并支持工具栏。 你可以重写 <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> 属性以返回所承载的控件的句柄。  
  
 可以将许多不同的功能添加到工具窗口。 例如，可以添加工具栏：[将工具栏添加到工具窗口](../extensibility/adding-a-toolbar-to-a-tool-window.md)或快捷菜单：[工具窗口中添加快捷菜单](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md)。 可以添加一个搜索控件，可用于搜索工具窗口中的项：[将搜索添加到工具窗口](../extensibility/adding-search-to-a-tool-window.md)。  
  
 您可以订阅事件的工具窗口：[订阅事件](../extensibility/subscribing-to-an-event.md)。  
  
## <a name="extending-existing-tool-windows"></a>扩展现有工具 Windows  
 可以将信息有关的工具窗口信息添加到一个新**选项**页和上的新设置**属性**页上，写入**任务列表**和**输出** windows。 有关详细信息，请参阅[扩展属性、 任务列表、 输出和选项 Windows](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)并[扩展属性、 任务列表、 输出和选项 Windows](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)。  
  
## <a name="modal-dialog-boxes"></a>模式对话框  
 在 Visual Studio 扩展中应创建模式对话框，通过从它们派生<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName>，可用于控制它们和其余的 UI。 有关详细信息，请参阅。 [创建和管理模式对话框](../extensibility/creating-and-managing-modal-dialog-boxes.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)
