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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180386"
---
# <a name="properties-display-grid"></a>属性显示网格
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

" **属性** " 窗口显示网格中的字段。 左侧列包含属性名称;右侧列包含属性值。  
  
## <a name="working-with-the-grid"></a>使用网格  
 两列列表显示了独立于配置的属性，这些属性可在设计时和当前设置中进行更改。 请注意，可能不会显示所有属性。 可以通过实现方法将属性设置为隐藏 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> 。 具体而言，若要隐藏具有子属性的属性，请参阅， [隐藏具有子属性的属性](../../misc/hiding-properties-that-have-child-properties.md)。  
  
 为了将信息推送到 " **属性** " 窗口，IDE 使用 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 由 Vspackage 为每个窗口调用，其中包含具有相关属性的可选择对象，这些对象将显示在 " **属性** " 窗口中。 **解决方案资源管理器** <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> `GetProperty` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 在项目层次结构中使用调用的实现，以获取层次结构中的可浏览对象。  
  
 如果 VSPackage 不支持 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> ，则 IDE 会尝试使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 层次结构项或项提供的值。  
  
 你的项目 VSPackage 无需创建， <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 因为 IDE 提供的用于实现它的窗口包 (例如， **解决方案资源管理器**) <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 代表其构造。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 由 IDE 调用的三个方法组成：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> 包含在 " **属性** " 窗口中选择要显示的对象的数目。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 返回在 `IDispatch` " **属性** " 窗口中选择要显示的对象。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 允许用户选择由返回的任何对象 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 。 这允许 VSPackage 以可视方式更新用户在 UI 中显示的选择。  
  
  " **属性** " 窗口从对象中提取信息 `IDispatch` 以检索要浏览的属性。 "属性浏览器" `IDispatch` 通过查询 `ITypeInfo` （从获取）来请求对象支持的属性 `IDispatch::GetTypeInfo` 。 然后，浏览器使用这些值来填充 " **属性** " 窗口，并更改网格中显示的各个属性的值。 属性信息在对象本身内维护。  
  
  由于返回的对象支持 `IDispatch` ，因此调用方可以通过调用 `IDispatch::Invoke` 或 `ITypeInfo::Invoke` 使用预定义的调度标识符（ (DISPID) 来表示所需的信息）来获取信息（如对象的名称）。 声明的 Dispid 为负数，以确保它们不会与用户定义的标识符冲突。  
  
  " **属性** " 窗口显示不同类型的字段，具体取决于所选对象的特定属性的属性。 这些字段包括编辑框、下拉列表和指向自定义编辑器对话框的链接。  
  
- 枚举列表中包含的值通过 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 查询来检索 `IDispatch` 。 在 "属性" 网格中，可以通过双击字段名称，或通过单击值并从下拉列表中选择新值来更改从枚举列表获得的值。 对于具有枚举列表中预定义的设置的属性，双击 "属性" 列表中的属性名称将循环访问可用选项。 对于仅有两个选项的预定义属性（如 true/false），请双击属性名称以在选项之间切换。  
  
- 如果 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A> 为 `false` ，指示值已更改，则该值显示为粗体文本。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> 用于确定是否可将值重置为原始值。 如果是这样，则可以通过右键单击值并从显示的菜单中选择 " **重置** "，来改回默认值。 否则，必须手动将该值改回默认值。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 还允许您本地化和隐藏在设计时显示的属性的名称，但不会影响运行时显示的属性名称。  
  
- 单击省略号 ( ") " 按钮将显示一个属性值列表，用户可从中选择 (，如颜色选取器或字体列表) 。 <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> 提供这些值。  
  
## <a name="see-also"></a>另请参阅  
 [扩展属性](../../extensibility/internals/extending-properties.md)
