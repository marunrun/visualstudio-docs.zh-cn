---
title: 向设计师提供撤消支持 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], undo support
ms.assetid: 43eb1f14-b129-404a-8806-5bf9b099b67b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0580f974c362a71c3e400946f2ad34f565ad1232
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699678"
---
# <a name="supply-undo-support-to-designers"></a>向设计人员提供撤消支持

设计人员（如编辑器）通常需要支持撤消操作，以便用户可以在修改代码元素时撤消其最近的更改。

在 Visual Studio 中实现的大多数设计人员都有环境自动提供的"撤消"支持。

需要为撤消功能提供支持的设计器实现：

- 通过实现抽象基类提供撤消管理<xref:System.ComponentModel.Design.UndoEngine>

- 通过实现<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>和<xref:System.ComponentModel.Design.IComponentChangeService>类来提供持久性和 CodeDOM 支持。

有关使用 .NET 框架编写设计器的详细信息，请参阅[扩展设计时间支持](/previous-versions/37899azc(v=vs.140))。

通过[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]以下选项提供默认撤消基础结构：

- 通过<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>和<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit>类提供撤消管理实现。

- 通过默认值<xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>和实现提供持久性和<xref:System.ComponentModel.Design.IComponentChangeService>CodeDOM 支持。

## <a name="obtain-undo-support-automatically"></a>自动获取撤消支持

在 Visual Studio 中创建的任何设计器都具有自动和完全撤消支持，如果：

- 使用<xref:System.Windows.Forms.Control>基于它的类进行用户界面。

- 使用基于 CodeDOM 的标准代码生成和分析系统来生成和持久化。

   有关使用 Visual Studio CodeDOM 支持的详细信息，请参阅[动态源代码生成和编译](/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation)。

## <a name="when-to-use-explicit-designer-undo-support"></a>何时使用显式设计器撤消支持
 如果设计人员使用图形用户界面（称为视图适配器）（而不是 提供 的<xref:System.Windows.Forms.Control>用户界面），则必须提供自己的撤消管理。

 例如，创建具有基于 Web 的图形设计界面而不是基于 .NET 框架的图形界面的产品。

 在这种情况下，需要使用 向<xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute>Visual Studio 注册此视图适配器，并提供显式撤消管理。

 如果设计人员不使用<xref:System.CodeDom>名称空间中提供的 Visual Studio 代码生成模型，则需要提供 CodeDOM 和持久性支持。

## <a name="undo-support-features-of-the-designer"></a>撤消设计器的支持功能
 环境 SDK 提供提供撤消支持所需的默认接口实现，设计人员可以使用这些支持，这些支持可用于不使用<xref:System.Windows.Forms.Control>基于其用户界面的类或标准 CodeDOM 和持久性模型。

 类<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>派生自 .NET Framework<xref:System.ComponentModel.Design.UndoEngine>类，使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>类的实现来管理撤消操作。

 Visual Studio 为设计器撤消提供了以下功能：

- 跨多个设计器链接的撤消功能。

- 设计器中的子单位可以通过实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit>和<xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit>在<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit>与其父母进行交互。

环境 SDK 通过提供以下功能提供 CodeDOM 和持久性支持：

- <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>作为<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

- 由<xref:System.ComponentModel.Design.IComponentChangeService>视觉工作室设计主机提供。

## <a name="use-the-environment-sdk-features-to-supply-undo-support"></a>使用环境 SDK 功能提供撤消支持

要获得撤消支持，实现设计器的对象必须实例化和初始化具有有效<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine><xref:System.IServiceProvider>实现的类的实例。 此类<xref:System.IServiceProvider>必须提供以下服务：

- <xref:System.ComponentModel.Design.IDesignerHost>.

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

   使用 Visual Studio CodeDOM 序列化的<xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>设计人员可以选择使用[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]作为 实现的<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>提供的 。

   在这种情况下，<xref:System.IServiceProvider>提供给构造函数的<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>类应返回此对象作为<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>类的实现。

- <xref:System.ComponentModel.Design.IComponentChangeService>

   使用 Visual <xref:System.ComponentModel.Design.DesignSurface> Studio 设计主机提供的默认值的设计人员保证具有<xref:System.ComponentModel.Design.IComponentChangeService>类的默认实现。

实现基于撤消<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>机制的设计人员在：

- 属性更改通过<xref:System.ComponentModel.TypeDescriptor>对象进行。

- <xref:System.ComponentModel.Design.IComponentChangeService>提交可撤消的更改时，将手动生成事件。

- 对设计器的修改是在 的上下文中创建的<xref:System.ComponentModel.Design.DesignerTransaction>。

- 设计<xref:System.ComponentModel.Design.UndoEngine.UndoUnit>器选择使用 实现提供的标准撤消单元或特定于 Visual Studio 的实现显式创建撤消单元，该单元<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit>派生<xref:System.ComponentModel.Design.UndoEngine.UndoUnit>并同时提供<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit>和<xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit>的实现。

## <a name="see-also"></a>请参阅

- <xref:System.ComponentModel.Design.UndoEngine>
- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>
- [扩展设计时间支持](/previous-versions/37899azc(v=vs.140))
