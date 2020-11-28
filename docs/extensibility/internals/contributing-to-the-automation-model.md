---
title: 参与自动化模型 |Microsoft Docs
description: 了解如何在设计 VSPackage 时遵循一组准则来参与 Visual Studio 自动化模型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab43da108a8d4a3339c54973f60bf1bef6a74780
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305592"
---
# <a name="contribute-to-the-automation-model"></a>参与自动化模型
Visual Studio 提供了一组用于自定义环境的自动化接口。 自动化模型是使最终用户能够创建 Visual Studio 外接程序和扩展的对象模型。

 此外，它还适合作为 VSPackage 开发人员，以参与自动化模型;通过执行此操作，你可以使 VSPackage 的最终用户能够创建外接程序，并且通常在使用 VSPackage 时提供一致的用户模型体验 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 为了使最终用户体验保持一致，你可以在设计 VSPackage 时遵循一组指导原则，以便 VSPackage 的自动化模型遵循中的观点 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="in-this-section"></a>在本节中
- [自动化模型概述](../../extensibility/internals/automation-model-overview.md)

 将自动化模型定义为一组相关对象，这些对象控制常见环境的主要方面。 此对象集在自动化模型的关系图中进行了图示。

- [为 Vspackage 提供自动化](../../extensibility/internals/providing-automation-for-vspackages.md)

 讨论提供 VSPackage 自动化的两种主要方法。

- [公开项目对象](../../extensibility/internals/exposing-project-objects.md)

 提供创建特定于 VSPackage 的对象的分步说明。

- [项目建模](../../extensibility/internals/project-modeling.md)

 介绍为新项目类型创建自动化所需的标准项目对象，并说明了项目自动化遵循的路径。 本主题还提供了类的声明和实现的列表。

- [公开事件](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)

 提供为自动化模型创建事件的分步说明。

- ["选项" 页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)

 介绍如何通过扩展对象，在 **工具** 菜单上返回 VSPackage 的 "自定义 **选项**" 对话框的支持属性的自动化对象 `DTE.Properties` 。

- [为代码提供自动化](../../extensibility/internals/providing-automation-for-code.md)

 说明不需要为代码创建自动化模型。 但在本主题中提供了一个链接，该链接提供了代码模型中的信息。

- [如何：为 Windows 提供自动化](../../extensibility/internals/how-to-provide-automation-for-windows.md)

 本文说明，当你想要使自动化对象在窗口中可用，并且环境尚未提供现成的自动化对象时，提供自动化是个好主意。 讨论工具窗口和文档窗口的自动化。

- [使用自动化模型](../../extensibility/internals/using-the-automation-model.md)

 提供两个代码示例，这些示例演示自动化使用者如何获取初始项目自动化对象。

- [Configuration 和 SelectedItem 对象的自动化](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)

 提供有关 Configuration 和 SelectedItems 对象的自动化的信息。

## <a name="reference"></a>参考
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 提供一个代码示例，该示例演示 VSPackage 如何参与 DTE 自动化对象模型。 列出参数、返回值和所选的备注。
