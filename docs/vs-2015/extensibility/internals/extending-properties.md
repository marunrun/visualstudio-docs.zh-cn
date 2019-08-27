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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690997"
---
# <a name="extending-properties"></a>扩展属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **属性**时段 COM 和 COM + 组件的通用属性浏览器，并且支持所有[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]产品。 **属性**窗口适用于`ITypeInfo`类型信息和 COM + 元数据以列出在集成的开发环境 (IDE) 中的任何其他窗口中的当前所选对象的设计时属性。  
  
 **属性**窗口中，也可以通过在键盘上按 F4 或选择打开**属性窗口**上**视图**菜单中，用于查看和编辑独立于配置的、 设计时属性和所选对象的事件。 解决方案和项目，与关联的依赖于配置的属性显示在[属性页](../../extensibility/internals/property-pages.md)。 有关详细信息，请参阅[NIB： 项目属性](https://msdn.microsoft.com/fb126574-24ad-4c96-9b2b-6e1f3879ba50)，[管理配置选项](../../extensibility/internals/managing-configuration-options.md)，并[NIB： 项目管理在项目中](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)。  
  
 ![属性窗口概述](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow")  
“属性”窗口  
  
 本部分提供关联到的各个区域的详细的信息**属性**窗口和必须实现的接口，然后调用来填充窗口。  
  
## <a name="in-this-section"></a>本节内容  
 [属性窗口概述](../../extensibility/internals/properties-window-overview.md)  
 说明的用途**属性**相对于工具窗口和文档窗口的窗口。  
  
 [模板策略和属性窗口](../../extensibility/internals/template-policy-and-the-properties-window.md)  
 讨论如何在企业模板项目中，包含一个项目，以及如何该企业级模板项目可以强制执行策略。  
  
 [属性窗口字段和界面](../../extensibility/internals/properties-window-fields-and-interfaces.md)  
 介绍了所选内容，用于确定在显示的信息的基础**属性**窗口。  
  
 [属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)  
 描述的目的**属性**窗口对象列表中，描述如何，此列表中的不同对象触发时调用，环境将得到通知，已选择一个新的对象。  
  
 [属性窗口按钮](../../extensibility/internals/properties-window-buttons.md)  
 说明显示在四个默认按钮的用途**属性**窗口工具栏。  
  
 [属性显示网格](../../extensibility/internals/properties-display-grid.md)  
 介绍了其中网格中找到的属性名称和属性值字段。  
  
 [宣布属性窗口选定内容跟踪](../../misc/announcing-property-window-selection-tracking.md)  
 介绍了选择跟踪**属性**窗口。  
  
 [隐藏具有子属性的属性](../../misc/hiding-properties-that-have-child-properties.md)  
 介绍如何隐藏具有子属性通过实现属性<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>接口。  
  
 [提供自定义属性窗口](../../misc/providing-a-custom-properties-window.md)  
 详细介绍了用于提供属性浏览器的步骤。  
  
 [从属性窗口中获取字段说明](../../misc/getting-field-descriptions-from-the-properties-window.md)  
 介绍在何处找到说明区域显示与所选的属性字段相关的信息。  
  
 [在“属性”窗口中更新属性值](../../misc/updating-property-values-in-the-properties-window.md)  
 提供了分步说明，显示两个方法可以保持**属性**窗口与属性值更改同步。  
  
## <a name="related-sections"></a>相关章节  
 [项目类型](../../extensibility/internals/project-types.md)  
 讨论项目的构建基块作为[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE。  
  
 [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)  
 介绍如何使用[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]持续测试和调试应用程序，在你生成应用的平台。  
  
 [HTML 文档属性，属性窗口](https://msdn.microsoft.com/library/46e3d164-a1a7-42f9-87b0-344e10a37b62)  
 提供编辑 HTML 文档直接从属性窗口的说明，并提供一个表详细列出在属性窗口中的 HTML 文档中的字段。  
  
 [IDispatch](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)  
 介绍`IDispatch`接口，它首先设计为支持自动化，提供了一个后期绑定机制来访问和检索有关方法和对象的属性的信息。  
  
 [NIB：介绍动态属性 (Visual Studio)](https://msdn.microsoft.com/f5102027-1431-4195-ae40-9b991de46d3a)  
 概述，您可以配置你的应用程序，以使属性值存储在外部配置文件而不是应用程序的已编译代码的动态属性。  
  
 [NIB： 项目作为容器](https://msdn.microsoft.com/87d40f63-f487-4767-8963-64beec27ba1b)  
 描述为一个解决方案来以逻辑方式管理、 生成和调试构成应用程序的各个项中的容器的项目的角色。  
  
 [NIB： 项目属性](https://msdn.microsoft.com/fb126574-24ad-4c96-9b2b-6e1f3879ba50)  
 介绍如何在项目管理设置，可将应用于整个项目的控件属性以及仅限于特定生成配置的项目的属性。  
  
 [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)  
 介绍了如何[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]有效地管理等的引用、 数据连接、 文件夹和文件所需的开发工作通过解决方案和项目项。  
  
 [扩展 Visual Studio 的其他部分](../../extensibility/extending-other-parts-of-visual-studio.md)  
 说明如何使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]的其余部分的 UI 元素。
