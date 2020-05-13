---
title: 视觉工作室的交互模式 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ac917aeb2530570b755e7f1e6fc6de00714a54b0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698375"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio 的交互模式
## <a name="overview"></a>概述
 通常，设计模式是设计的核心，可用于特定情况，以解决具有类似约束集的问题。 功能和系统设计人员使用这些设计模式作为起点，然后可以根据具体情况进行调整。

 Visual Studio 具有一个常见交互模式库，在构建新功能时应考虑这些模式。 我们的设计模式有两个核心上下文：视觉工作室客户端 （devenv） 和可视化工作室在线。 对于某些设计问题，有一种无处不在的模式，在所有情况下都效果很好。 但是，在许多情况下，对于在浏览器中显示的 UI 和托管在客户端应用程序上的 UI，解决方案可能有所不同。

### <a name="visual-studio-client-pattern-types"></a>可视化工作室客户端模式类型

|模式类型|描述|示例|
|------------------|-----------------|--------------|
|**应用程序级模式**|应用程序共有的高级模式，确定或显示应用程序上下文，并在其中包含复合和控制模式|- 工具窗口<br />- 文档窗口|
|**复合模式**|跨应用程序模式的常见模式，或由不同配置中的多个控件组成的识别模式|- 查看切换<br />- 列表生成器<br />- 显示数据<br />- 通知<br />- 验证<br />- 选择模型|
|**控制模式**|关于低级控件预期如何操作的具体细节|- 树视图<br />- 在网格控件内编辑|

## <a name="application-patterns"></a>应用程序模式
 在高级别上，Visual Studio 界面包含单个 IDE 中的多个窗口、对话框、命令和工具栏。 Visual Studio 层次结构确定上下文并驱动菜单。 IDE 用户界面中的关键集成点是文档窗口、工具窗口、项目、命令结构、文本编辑器、工具箱、属性窗口和工具>选项。

 IDE 用户界面中的每个关键集成点都有基本使用模式：

- [Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [窗互](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [工具窗口](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [文档编辑器约定](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [项目](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>常见的控制模式
 控制模式主要涉及单个控件的可预期方式。 这是一致性最关键的一个领域。

 可视化工作室中最常见的控件应遵循桌面 Windows 指南。 我们的指南仅包括我们需要通过 Visual Studio 特定交互来增强常见约定的领域，或者我们完全取代准则的位置，以便定制 Visual Studio 以满足我们老练用户的需求。

- [Visual Studio 的公共控件模式](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [常见控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>复合模式
 用户期望通过多种方式完成任务。 在可能的情况下，应设计要素以将这些模式用于交互和可视化设计。

 虽然 Visual Studio 中有许多复合模式，但有关一致性的一些最重要的模式是：

- [Visual Studio 的复合模式](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [对象 UI 和窥视](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [选择模型](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [持久性和保存设置](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [触摸输入](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
