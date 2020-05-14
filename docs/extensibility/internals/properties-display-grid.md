---
title: 属性显示网格 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d094c32ba8a64fc636f3fb6dfb2944dc3955628a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706185"
---
# <a name="properties-display-grid"></a>属性显示网格

"**属性"** 窗口显示网格中的字段。 左列包含属性名称;第二列包含属性名称。右列包含属性值。

## <a name="work-with-the-grid"></a>使用网格

两列列表显示可在设计时间更改的与配置无关的属性及其当前设置。 请注意，可能无法显示所有属性。 属性可以设置为隐藏，例如，通过实现 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A>。 具体而言，要隐藏具有子属性的属性：

1. 将`pfDisplay`参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A>设置为`FALSE`。

2. 将`pfHide`参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A>设置为`TRUE`。

要将信息推送到 **"属性"** 窗口，IDE<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>将使用 。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>VSPackages 为包含要在 **"属性"** 窗口中显示的相关属性的可选对象的每个窗口调用 VSPackages。 **解决方案资源管理器**使用__VSHPROPID实现<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>调用`GetProperty`[。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)项目层次结构中获取层次结构中的可浏览对象。

如果您的 VS 包不支持[__VSHPROPID。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)，IDE 尝试使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>[值__VSHPROPID。VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>)层次结构项或项供应。

项目 VSPackage 不需要创建<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>，因为实现它的 IDE 提供的窗口包（例如，**解决方案资源管理器**）<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>代表它构造。

<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>由 IDE 调用的三种方法组成：

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A>包含选择要在 **"属性"** 窗口中显示的对象数。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>返回选择要`IDispatch`在 **"属性"** 窗口中显示的对象。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A>使返回的任何对象<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>都成为可能，由用户选择。 这允许 VSPackage 直观地更新在 UI 中显示的选择。

属性**窗口**从`IDispatch`对象中提取信息以检索正在浏览的属性。 属性浏览器用于`IDispatch`通过查询`ITypeInfo`（从 中`IDispatch::GetTypeInfo`获取）询问对象支持的属性。 然后，浏览器使用这些值填充 **"属性"** 窗口并更改网格中显示的单个属性的值。 属性信息在对象本身中维护。

由于返回的对象支持`IDispatch`，因此调用方可以通过调用或`IDispatch::Invoke``ITypeInfo::Invoke`使用表示所需信息的预定义调度标识符 （DISPID） 来获取对象名称等信息。 声明的 DISPID 为负值，以确保它们不与用户定义的标识符冲突。

属性**窗口**显示不同类型的字段，具体取决于所选对象的特定属性的属性。 这些字段包括编辑框、下拉列表和指向自定义编辑器对话框的链接。

- 枚举列表中包含的值由<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>查询`IDispatch`检索到 。 通过双击字段名称，或者单击该值并从下拉列表中选择新值，可以在属性网格中更改从枚举列表中获取的值。 对于具有枚举列表中预定义设置的属性，双击"属性"列表中的属性名称会循环浏览可用选项。 对于只有两个选项的预定义属性（如真/假），双击属性名称在选项之间切换。

- 如果<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A>`false`为 ，指示该值已更改，则该值以粗体文本显示。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A>用于确定该值是否可以重置为原始值。 如果是这样，您可以通过右键单击值并从显示的菜单中选择 **"重置"** 来更改回默认值。 否则，您必须手动将值更改回默认值。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>还允许您本地化和隐藏设计期间显示的属性的名称，但不会影响运行时显示的属性名称。

- 单击省略号 （...） 按钮将显示用户可以从中选择的属性值列表（如颜色选取器或字体列表）。 <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>提供这些值。

## <a name="see-also"></a>请参阅

- [扩展属性](../../extensibility/internals/extending-properties.md)
