---
title: Visual Studio 的交互模式 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bfa0a25eac1c14c1d07096840b88a1ec63593f56
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824304"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio 的交互模式
## <a name="overview"></a>概述
 一种设计模式，一般情况下，是设计的可以应用在特定情况下，若要解决问题的约束类似集合的核心。 功能和系统设计器使用这些设计模式作为起始点，然后可适用于其特定的情况。

 Visual Studio 提供生成的新功能时应考虑的常见交互模式的库。 有两个核心上下文为我们的设计模式：Visual Studio 客户端 (devenv) 和 Visual Studio Online。 对于某些设计问题，是适用于所有情况下的通用模式。 在许多情况下，但是，解决方案可能是不同的在浏览器并且将托管在客户端应用程序上显示的 UI。

### <a name="visual-studio-client-pattern-types"></a>Visual Studio 客户端模式类型

|模式类型|描述|示例|
|------------------|-----------------|--------------|
|**应用程序级模式**|通用的应用程序，确定或显示应用程序上下文中，并包含其中的复合和控件模式的高级模式|-工具窗口<br />-文档窗口|
|**复合模式**|可能会跨应用程序模式的常见模式或识别的模式的不同配置中的多个控件组成|视图切换<br />列表生成器<br />-显示数据<br />-通知<br />验证<br />选择模型|
|**控件模式**|有关如何低级别的控件的具体信息应表现出的行为|树视图<br />-网格控件中编辑|

## <a name="application-patterns"></a>应用程序模式
 在高级别中，Visual Studio 界面包含多个 windows、 对话框、 命令和单个 IDE 中的工具栏。 Visual Studio 层次结构确定上下文和驱动器菜单。 IDE 的用户界面的关键集成点是文档窗口： 工具窗口、 项目、 命令结构、 文本编辑器、 工具箱、 属性窗口中和工具 > 选项。

 有基本的使用模式为每个用户界面中的 IDE 的关键集成点：

- [Visual Studio 的菜单和命令](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [窗口的交互](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [工具窗口](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [文档编辑器约定](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [对话框](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [项目](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>常见控件模式
 控件模式主要是关于个别控件预期行为。 这是一个在其中一致性是最关键的区域。

 在 Visual Studio 中最常用的控件应遵循的桌面 Windows 准则。 我们的指导原则只包括我们需要增加使用的特定于 Visual Studio 的交互或在其中我们取代准则完全为了定制 Visual Studio 以满足我们经验丰富的用户的需求的位置的常见约定领域。

- [Visual Studio 的公共控件模式](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [常见控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>复合模式
 有许多用户希望在完成任务的方法。 如有可能，应设计功能来使用这些模式为交互和可视化设计。

 尽管有很多的复合模式，在 Visual Studio 中，一些最重要的方面的一致性是：

- [Visual Studio 的复合模式](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [对象上的 UI 和扫视](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [选择模型](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [持久性和保存设置](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [触摸输入](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
