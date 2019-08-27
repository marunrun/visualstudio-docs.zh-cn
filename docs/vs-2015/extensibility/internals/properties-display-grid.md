---
title: 属性显示网格 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5fd5e17d764336cda450c726023b209f89f194a1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180386"
---
# <a name="properties-display-grid"></a>属性显示网格
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**属性**窗口将显示在网格中的字段。 左侧的列包含的属性名称;右侧列包含的属性值。  
  
## <a name="working-with-the-grid"></a>使用网格  
 两个列列表显示了在设计时和其当前设置进行更改的独立于配置的属性。 请注意，可能不会显示所有属性。 属性可以设置为隐藏，例如，通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A>方法。 具体而言，到具有子属性，请参阅的隐藏属性[隐藏属性，具有子属性](../../misc/hiding-properties-that-have-child-properties.md)。  
  
 信息推送到**属性**窗口中，IDE 使用<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 由每个窗口，其中包含具有要显示在相关属性的可选择对象的 Vspackage**属性**窗口。 **解决方案资源管理器**的实现<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>调用`GetProperty`使用<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>项目层次结构来获取层次结构中的可浏览对象中。  
  
 如果你的 VSPackage 不支持<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>，尝试使用 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>使用的值为<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>提供层次结构项。  
  
 你的项目不需要创建 VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>因为实现该 IDE 提供窗口包 (例如，**解决方案资源管理器**) 构造<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>代表其自身。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 包含由 IDE 调用的三种方法：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> 包含选择要在中显示的对象数**属性**窗口。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 返回`IDispatch`选择要在中显示的对象**属性**窗口。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 使返回的任何的对象<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>供选择的用户。 这使 VSPackage 可以直观地更新 UI 中向用户显示的选项。  
  
  **属性**窗口中提取信息从`IDispatch`对象来检索正在被浏览的属性。 属性浏览器使用`IDispatch`向对象要求哪些属性它支持通过查询`ITypeInfo`，从中获取从`IDispatch::GetTypeInfo`。 在浏览器并将这些值来填充**属性**窗口并更改网格中显示单个属性的值。 属性信息保留在对象本身。  
  
  因为返回的对象支持`IDispatch`，调用方可以通过调用获取信息，如对象的名称`IDispatch::Invoke`或`ITypeInfo::Invoke`与表示所需的信息的预定义的调度标识符 (DISPID)。 声明的 Dispid 为负，以确保它们不会与用户定义的标识符发生冲突。  
  
  **属性**窗口会显示不同类型的字段，具体取决于所选对象的特定属性的属性。 这些字段包括编辑框、 下拉列表和指向自定义编辑器对话框。  
  
- 检索的枚举列表中包含值<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>查询到`IDispatch`。 获取从枚举列表值可以更改在属性网格中，通过双击字段名称，或通过单击值并从下拉列表中选择新值。 对于具有预定义的枚举列表中的设置的属性，双击属性列表中的属性名称进行循环的可用选项。 只有两个选项，如 true/false 时，使用预定义属性中，双击要选项之间进行切换的属性名称。  
  
- 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A>是`false`，表示的值已更改，以粗体显示的值。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> 用于确定是否值可以重置为原始值。 如果因此，您可以改回为默认值通过右键单击该值，然后选择**重置**从显示的菜单。 否则，必须手动更改回默认值的值。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 此外允许您以本地化和隐藏在设计时显示的属性的名称，但不会影响在运行时显示的属性名称。  
  
- 单击省略号 （...） 按钮显示的用户可以从中选择 （如颜色选取器或字体列表） 的属性值的列表。 <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> 提供这些值。  
  
## <a name="see-also"></a>请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)
