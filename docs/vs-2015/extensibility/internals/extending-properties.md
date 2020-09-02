---
title: 扩展属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b5d2e7d15f7b479941c3186d8cd694c92f762bbf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65690997"
---
# <a name="extending-properties"></a>扩展属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

" [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **属性** " 窗口是 COM 和 com + 组件的通用属性浏览器，支持所有 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 产品。 " **属性** " 窗口与 `ITypeInfo` 类型信息和 com + 元数据一起使用，以便在集成开发环境 (IDE) 的任何其他窗口中列出当前所选对象的设计时属性。  
  
 可以通过按键盘上的 F4 或选择 "**视图**" 菜单上的 "**属性" 窗口**打开的 "**属性**" 窗口，用于查看和编辑所选对象的独立于配置的、设计时属性和事件。 与解决方案和项目关联的配置相关属性将显示在 [属性页](../../extensibility/internals/property-pages.md)上。 有关详细信息，请参阅 [笔尖：项目属性](https://msdn.microsoft.com/fb126574-24ad-4c96-9b2b-6e1f3879ba50)、 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)和 [笔尖：项目中的项管理](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)。  
  
 ![属性窗口概述](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow")  
“属性”窗口  
  
 本节提供的详细信息与 " **属性** " 窗口的各个区域以及您必须实现并调用以填充窗口的接口相关。  
  
## <a name="in-this-section"></a>本节内容  
 [属性窗口概述](../../extensibility/internals/properties-window-overview.md)  
 说明 " **属性** " 窗口相对于工具窗口和文档窗口的用途。  
  
 [模板策略和属性窗口](../../extensibility/internals/template-policy-and-the-properties-window.md)  
 讨论一个项目如何包含在企业模板项目中，以及该企业模板项目如何强制实施策略。  
  
 [Properties Window Fields and Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)  
 说明用于确定 " **属性** " 窗口中显示的信息的选择的基础。  
  
 [属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)  
 描述 " **属性** " 窗口对象列表的用途，描述如何，当此列表中的不同对象触发调用时，将通知环境已选择了新的对象。  
  
 [属性窗口按钮](../../extensibility/internals/properties-window-buttons.md)  
 说明 " **属性** " 窗口工具栏上显示的四个默认按钮的用途。  
  
 [属性显示网格](../../extensibility/internals/properties-display-grid.md)  
 说明在网格中找到属性名称和属性值字段的位置。  
  
 [宣布属性窗口选定内容跟踪](../../misc/announcing-property-window-selection-tracking.md)  
 描述 " **属性** " 窗口的选择跟踪。  
  
 [隐藏具有子属性的属性](../../misc/hiding-properties-that-have-child-properties.md)  
 说明如何通过实现接口隐藏具有子属性的属性 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 。  
  
 [提供自定义属性窗口](../../misc/providing-a-custom-properties-window.md)  
 详细介绍提供您自己的属性浏览器的步骤。  
  
 [从属性窗口中获取字段说明](../../misc/getting-field-descriptions-from-the-properties-window.md)  
 说明在何处可以找到显示与所选属性字段相关的信息的说明区域。  
  
 [在“属性”窗口中更新属性值](../../misc/updating-property-values-in-the-properties-window.md)  
 提供显示两种方法的分步说明，使 " **属性** " 窗口与属性值更改保持同步。  
  
## <a name="related-sections"></a>相关章节  
 [项目类型](../../extensibility/internals/project-types.md)  
 讨论作为 IDE 构建基块的项目 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)  
 介绍如何使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 平台在生成应用程序时对其进行连续测试和调试。  
  
 [“属性”窗口 -&gt; HTML 文档属性](https://msdn.microsoft.com/library/46e3d164-a1a7-42f9-87b0-344e10a37b62)  
 提供直接从属性窗口编辑 HTML 文档的说明，并提供一个表，其中详细列出了属性窗口的 HTML 文档中的字段。  
  
 [IDispatch](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)  
 介绍 `IDispatch` 接口，该接口最初旨在支持自动化，提供一种后期绑定机制来访问和检索对象的方法和属性的相关信息。  
  
 [笔尖： (Visual Studio 的动态属性简介) ](https://msdn.microsoft.com/f5102027-1431-4195-ae40-9b991de46d3a)  
 概述允许您配置应用程序以便将属性值存储在外部配置文件而不是应用程序的编译代码中的动态属性。  
  
 [NIB：项目作为容器](https://msdn.microsoft.com/87d40f63-f487-4767-8963-64beec27ba1b)  
 描述项目在解决方案中的角色，以逻辑方式管理、生成和调试构成应用程序的项。  
  
 [钢笔尖：项目属性](https://msdn.microsoft.com/fb126574-24ad-4c96-9b2b-6e1f3879ba50)  
 描述项目如何管理设置，这些设置可让你控制应用于整个项目的属性，以及限制为项目的某些生成配置的属性。  
  
 [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)  
 说明如何 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 有效地管理通过解决方案和项目进行开发工作所需的项（如引用、数据连接、文件夹和文件）。  
  
 [扩展 Visual Studio 的其他部分](../../extensibility/extending-other-parts-of-visual-studio.md)  
 说明如何使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]的其余部分的 UI 元素。
