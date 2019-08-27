---
title: 属性窗口概述 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05c772365c42037bfd97a2a31b80efc2f5f1a48b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347819"
---
# <a name="properties-window-overview"></a>属性窗口概述
**属性**窗口用于显示在 windows 中可用的两个主要类型中选择的对象的属性[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE)。 Windows 这两种类型是：

- 如解决方案资源管理器、 类视图和对象浏览器的工具窗口

- 包含此类编辑器和设计器为窗体设计器、 XML 编辑器和 HTML 编辑器的文档窗口

## <a name="using-the-properties-window"></a>使用属性窗口
 **属性**窗口显示单个或多个选定的项的属性。 如果选择了多个项，会显示所有选定对象的所有属性的交集。

 中会显示与所选对象中的窗体设计窗口或 HTML 编辑器使用 COM + 元数据相关的事件**属性**窗口。 例如，可以选择一个按钮，并显示其关联的事件，如`OnClick`事件，可以链接到该按钮。

 在显示事件**属性**窗口主要用于绑定到代码的对象。 如果正在编辑没有执行任何操作，代码的文件格式，您都不会有任何事件。 中仅显示事件**属性**窗口时运行代码，并具有特定的对象关联的某些事件之间的绑定。 此示例将代码隐藏所选对象时激活该对象执行。

 下表列出了使用的主接口**属性**窗口。

|接口名称|描述|
|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|提供了一系列为类别**属性**窗口，并将每个属性映射到某个类别。|
|[IDispatch 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)|公开对象的方法和属性到编程的工具和其他应用程序支持自动化。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|提供了名为的省略号 （...） 按钮*生成器*的打开模式对话框窗口本身的对象实现。 在文本字段中用户无法轻松地键入一个值时使用。 例如，它可能会用于打开颜色选取器，用于确定为你的 RGB 值。|
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|提供对用于更新中显示信息的对象的访问**属性**窗口。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 是为每个窗口，其中包含要显示相关属性与可选择对象实现的 Vspackage。|
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|提供有关如方法的对象类型的接口和结构的字段的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|允许 Vspackage 接收通知的选中内容事件以及如何检索有关当前项目层次结构、 项、 元素值和命令 UI 上下文信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|提供有权访问多个选择的环境。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|用于提供对某些属性中显示的本地化的名称**属性**窗口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|通知对当前所选内容中，元素值或命令 UI 上下文的更改已注册的 Vspackage。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|发送通知的当前选定内容中更改环境，并提供对与新的所选内容相关的层次结构和项信息的访问。|

 有关详细信息`IDispatch`，请参阅 MSDN 库。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
- [属性窗口字段和界面](../../extensibility/internals/properties-window-fields-and-interfaces.md)