---
title: Visual Studio 的交互模式 |Microsoft Docs
ms.date: 05/13/2020
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5cbfeef3352e4abd03e12cc6b228cea8a8c124a6
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184401"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio 的交互模式
## <a name="overview"></a>概述
 通常，设计模式是设计的核心，它可以在特定情况下应用以解决类似约束集的问题。 功能和系统设计器使用这些设计模式作为起点，然后可以根据具体情况调整这些起点。

 Visual Studio 具有一个通用交互模式库，在生成新功能时应考虑到这些模式。 设计模式有两个核心上下文： Visual Studio 客户端（devenv）和 Visual Studio Codespaces （以前称为 Visual Studio Online）。 对于某些设计问题，有一种广泛的模式适用于所有情况。 但是，在许多情况下，对于在浏览器中呈现的 UI，以及在客户端应用程序上承载的 UI，解决方案可能会有所不同。

### <a name="visual-studio-client-pattern-types"></a>Visual Studio 客户端模式类型

|模式类型|描述|示例|
|------------------|-----------------|--------------|
|**应用程序级模式**|应用程序通用的高级模式，确定或显示应用程序上下文，并在其中包含复合和控件模式|-工具窗口<br />-文档窗口|
|**复合模式**|可能跨应用程序模式的常见模式，或在不同配置中由多个控件组成的可识别模式|-查看切换<br />-列表生成器<br />-显示数据<br />-通知<br />-验证<br />-选择模型|
|**控件模式**|有关底层控件应如何表现的详细信息|-树形视图<br />-在 grid 控件内编辑|

## <a name="application-patterns"></a>应用程序模式
 在高级别上，Visual Studio 接口在单个 IDE 内包含多个窗口、对话框、命令和工具栏。 Visual Studio 层次结构决定了上下文和驱动器菜单。 IDE 用户界面中的关键集成点包括文档窗口、工具窗口、项目、命令结构、文本编辑器、工具箱、属性窗口和工具 > 选项。

 IDE 用户界面中的每个关键集成点都有基本的使用模式：

- [Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [窗口交互](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [工具窗口](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [文档编辑器约定](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [投射](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>公共控件模式
 控件模式主要涉及各个控件的行为方式。 这是一致性最为重要的一个领域。

 Visual Studio 中的最常见控件应遵循桌面 Windows 指导原则。 本指南仅包括一些区域，在这些区域中我们需要增加常见约定与 Visual Studio 的特定交互，或者我们完全取代了这些指导原则，以便为 Visual Studio 定制，以满足复杂用户的需求。

- [Visual Studio 的公共控件模式](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [常见控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>复合模式
 用户需要通过多种方式来完成任务。 只要有可能，功能就应该设计为使用这些模式进行交互和可视化设计。

 尽管在 Visual Studio 中有很多复合模式，但对于一致性而言，最重要的是：

- [Visual Studio 的复合模式](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [对象上的 UI 和扫视](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [选择模型](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [持久性和保存设置](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [触摸输入](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
