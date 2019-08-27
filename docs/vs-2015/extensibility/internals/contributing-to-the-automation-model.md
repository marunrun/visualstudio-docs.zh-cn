---
title: 自动化模型的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c84ea078f9b7c1268b765111cc400f6e51b783f1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196994"
---
# <a name="contributing-to-the-automation-model"></a>Contributing to the Automation Model
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 提供一组自动化接口的自定义环境。 自动化模型是使最终用户能够创建 Visual Studio 加载项和扩展的对象模型。  
  
 此外，它是适用于你，作为 VSPackage 开发人员，以参与自动化模型中;通过执行此操作，启用你的 VSPackage 创建外接程序，并通常提供一致的用户模型体验，在使用你的 VSPackage 中时的最终用户[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 为了使最终用户体验一致，可以遵循一组的指导原则，如设计你的 VSPackage，使你的 VSPackage 的自动化模型遵循中的观点[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
## <a name="in-this-section"></a>本节内容  
 [自动化模型概述](../../extensibility/internals/automation-model-overview.md)  
 定义为相关的一组对象，用于控制常见环境的主要方面的自动化模型。 此组对象的自动化模型的关系图中所示。  
  
 [提供适用于 VSPackage 的自动化](../../extensibility/internals/providing-automation-for-vspackages.md)  
 讨论两种主要的方法，以提供你的 VSPackage 的自动化。  
  
 [公开项目对象](../../extensibility/internals/exposing-project-objects.md)  
 提供用于创建特定于 VSPackage 的对象的分步说明。  
  
 [项目建模](../../extensibility/internals/project-modeling.md)  
 介绍创建新项目类型的自动化所需的标准项目对象，并说明了项目自动化遵循的路径。 本主题还提供了声明和实现对于类的列表。  
  
 [公开事件](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)  
 提供用于创建事件为您的自动化模型的分步说明。  
  
 [选项页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)  
 介绍如何为支持的 VSPackage 的属性的自定义返回自动化对象**选项**上的对话框中**工具**菜单上的，通过扩展`DTE.Properties`对象。  
  
 [提供适用于 Code 的自动化](../../extensibility/internals/providing-automation-for-code.md)  
 介绍了创建自动化模型为你的代码不需要。 但是，在此主题，它提供到代码模型中的深度信息中提供的链接。  
  
 [如何：提供适用于 Windows 的自动化](../../extensibility/internals/how-to-provide-automation-for-windows.md)  
 介绍了，无论何时你想要使自动化对象在一个窗口，并在环境不提供现成的自动化对象，提供自动化是一个不错的主意。 讨论了自动化的工具窗口和文档窗口。  
  
 [使用自动化模型](../../extensibility/internals/using-the-automation-model.md)  
 提供了两个代码示例演示如何自动化使用者获取初始项目自动化对象。  
  
 [Configuration 和 SelectedItem 对象的自动化](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)  
 提供有关配置选项的自动化和自动化的所选的项目信息。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>  
 提供的代码示例，演示如何在 DTE 自动化对象模型中加入 VSPackage。 列出了参数、 返回值和所选的备注。  
  
## <a name="related-sections"></a>相关章节
