---
title: 属性窗口概述 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 445a43cec976f363873c89dfe9b8e05429aebaf2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706033"
---
# <a name="properties-window-overview"></a>属性窗口概述
属性**窗口**用于显示[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在集成开发环境 （IDE） 中可用的两种主要窗口类型中选择的对象的属性。 这两种类型的窗口是：

- 工具窗口，如解决方案资源管理器、类视图和对象浏览器

- 包含表单设计器、XML 编辑器和 HTML 编辑器等编辑器和设计器的文档窗口

## <a name="using-the-properties-window"></a>使用属性窗口
 "**属性"** 窗口显示单个或多个选定项的属性。 如果选择了多个项，将显示所有选定对象的所有属性的交集。

 与窗体设计窗口中的选定对象相关的事件或使用 COM+ 元数据的 HTML 编辑器将显示在 **"属性"** 窗口中。 例如，您可以选择一个按钮并显示其关联的事件，如事件`OnClick`，该事件可以链接到该按钮。

 **属性**窗口中显示的事件主要与绑定到代码的对象一起使用。 如果要编辑与代码无关的文件格式，则不会有任何事件。 仅当正在运行的代码与与特定对象关联的某些事件之间存在绑定时，事件才会显示在 **"属性"** 窗口中。 例如，在激活该对象时执行的选定对象后面的代码。

 下表列出了**属性**窗口使用的主要接口。

|接口名称|描述|
|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|向 **"属性"** 窗口提供类别列表，并将每个属性映射到类别。|
|[I调度接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)|向支持自动化的编程工具和其他应用程序公开对象的方法和属性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|提供称为生成器的椭圆 （...） 按钮，这些*生成器*打开由对象本身实现的模式对话框窗口。 当用户不容易在文本字段中键入值时使用。 例如，它可用于打开一个颜色选取器，确定 RGB 值。|
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|提供对用于更新 **"属性"** 窗口中显示的信息的对象的访问。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>由 VSPackages 为每个包含要显示相关属性的可选对象的窗口实现。|
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|提供有关对象类型的信息，例如接口的方法和结构的字段。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|使 VSPackages 能够接收选择事件的通知，并检索有关当前项目层次结构、项、元素值和命令 UI 上下文的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|为环境提供对多个选择的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|用于在 **"属性"** 窗口中显示的某些属性上提供本地化名称。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|通知已注册的 VS 包对当前选择、元素值或命令 UI 上下文的更改。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|通知环境当前所选内容的变化，并提供对与新选择相关的层次结构和项目信息的访问。|

 有关 的详细信息`IDispatch`，请参阅 MSDN 库。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
- [属性窗口字段和界面](../../extensibility/internals/properties-window-fields-and-interfaces.md)
