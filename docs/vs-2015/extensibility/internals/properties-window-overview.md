---
title: "\"属性\" 窗口概述 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fd4be229338d1a09c22b4d81384dc90f0544fa39
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700746"
---
# <a name="properties-window-overview"></a>属性窗口概述
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

" **属性** " 窗口用于显示在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 集成开发环境 (IDE) 中可用的两种主要类型的 windows 中所选对象的属性。 这两种类型的窗口是：  
  
- 工具窗口，如解决方案资源管理器、类视图和对象浏览器  
  
- 文档窗口，其中包含这些编辑器和设计器作为窗体设计器、XML 编辑器和 HTML 编辑器  
  
## <a name="using-the-properties-window"></a>使用 "属性" 窗口  
 " **属性** " 窗口显示单个或多个选定项的属性。 如果选择了多个项，则会显示所有选定对象的所有属性的交集。  
  
 在 " **属性** " 窗口中显示与窗体设计窗口内的所选对象或使用 com + 元数据的 HTML 编辑器相关的事件。 例如，您可以选择一个按钮并显示其关联事件，例如 `OnClick` 事件，这些事件可以链接到该按钮。  
  
 " **属性** " 窗口中显示的事件主要用于绑定到代码的对象。 如果正在编辑的文件格式不包含任何与代码有关的内容，则不会有任何事件。 当运行代码和特定的事件与特定对象相关联时，事件仅显示在 " **属性** " 窗口中。 这种情况的一个示例是在激活对象时执行的所选对象的代码。  
  
 下表列出了 " **属性** " 窗口使用的主要接口。  
  
|接口名称|说明|  
|--------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|提供 " **属性** " 窗口的类别列表，并将每个属性映射到一个类别。|  
|[IDispatch 接口](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5)|向支持自动化的编程工具和其他应用程序公开对象的方法和属性。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|提供省略号 ( ... ) 称为 *生成器* 的按钮，这些按钮用于打开由对象本身实现的模式对话框窗口。 当用户在文本字段中无法轻松地键入值时使用。 例如，它可用于打开一个颜色选取器，用于确定您的 RGB 值。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|提供对用于更新 " **属性** " 窗口中显示的信息的对象的访问。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 为每个窗口实现 Vspackage，其中包含具有要显示的相关属性的可选择对象。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|提供有关对象类型（如接口的方法和结构的字段）的信息。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|允许 Vspackage 接收选择事件的通知，并检索有关当前项目层次结构、项、元素值和命令 UI 上下文的信息。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|为环境提供对多个选择的访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|用于在 " **属性** " 窗口中显示的某些属性上提供本地化的名称。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|通知注册的 Vspackage 当前选择、元素值或命令 UI 上下文的更改。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|向环境通知当前所选内容的更改，并提供对与新选择相关的层次结构和项信息的访问权限。|  
  
 有关的详细信息 `IDispatch` ，请参阅 MSDN library。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)   
 [Properties Window Fields and Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)
