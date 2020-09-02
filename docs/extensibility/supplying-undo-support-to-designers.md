---
title: 为设计器提供撤消支持 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699678"
---
# <a name="supply-undo-support-to-designers"></a>为设计器提供撤消支持

设计器（如编辑器）通常需要支持撤消操作，以便用户可以在修改代码元素时反转最近的更改。

在 Visual Studio 中实现的大多数设计器都由环境自动提供 "撤消" 支持。

需要为 undo 功能提供支持的设计器实现：

- 通过实现抽象基类来提供撤消管理 <xref:System.ComponentModel.Design.UndoEngine>

- 通过实现和类提供持久性和 CodeDOM <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> 支持  <xref:System.ComponentModel.Design.IComponentChangeService> 。

有关使用 .NET Framework 编写设计器的详细信息，请参阅 [扩展设计时支持](/previous-versions/37899azc(v=vs.140))。

[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]通过以下方式提供默认的撤消基础结构：

- 通过和类提供撤消管理 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> 实现 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> 。

- 通过默认和实现提供持久性和 CodeDOM <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> 支持 <xref:System.ComponentModel.Design.IComponentChangeService> 。

## <a name="obtain-undo-support-automatically"></a>自动获取撤消支持

如果为，则在 Visual Studio 中创建的任何设计器都具有自动和完全撤消支持：

- 使用 <xref:System.Windows.Forms.Control> 基于的类作为其用户界面。

- 采用基于 CodeDOM 的标准代码生成和分析系统，实现代码生成和持久性。

   有关使用 Visual Studio CodeDOM 支持的详细信息，请参阅 [动态源代码生成和编译](/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation)。

## <a name="when-to-use-explicit-designer-undo-support"></a>何时使用显式设计器撤消支持
 如果设计人员使用图形用户界面（称为视图适配器，而不是由提供的用户界面），则必须提供其自己的撤消管理 <xref:System.Windows.Forms.Control> 。

 例如，可以使用基于 web 的图形设计界面而不是基于 .NET Framework 的图形界面来创建产品。

 在这种情况下，需要使用 Visual Studio 注册此视图适配器 <xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute> ，并提供显式撤消管理。

 如果设计人员未使用命名空间中提供的 Visual Studio code 生成模型，则需要提供 CodeDOM 和持久性支持 <xref:System.CodeDom> 。

## <a name="undo-support-features-of-the-designer"></a>设计器的撤消支持功能
 环境 SDK 提供了提供撤消支持所需的接口的默认实现，设计器可以使用这些接口，而不是将 <xref:System.Windows.Forms.Control> 基于类的类用于其用户界面或标准 CodeDOM 和持久性模型。

 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>类派生自 .NET Framework <xref:System.ComponentModel.Design.UndoEngine> 类，该类使用类的实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> 来管理撤消操作。

 Visual Studio 提供了以下用于设计器撤消的功能：

- 跨多个设计器的链接撤消功能。

- 设计器中的子单元可通过实现和来与其父级交互 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> 。

环境 SDK 提供了 CodeDOM 和持久性支持，方法是提供：

- <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> 作为的实现 <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

- <xref:System.ComponentModel.Design.IComponentChangeService>由 Visual Studio 设计宿主提供的。

## <a name="use-the-environment-sdk-features-to-supply-undo-support"></a>使用环境 SDK 功能提供撤消支持

若要获取撤消支持，实现设计器的对象必须使用有效的实现来实例化和初始化类的实例 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:System.IServiceProvider> 。 此 <xref:System.IServiceProvider> 类必须提供以下服务：

- <xref:System.ComponentModel.Design.IDesignerHost>.

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

   使用 Visual Studio CodeDOM 序列化的设计器可以选择使用随 <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> 提供的 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 作为其实现的 <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> 。

   在这种情况下， <xref:System.IServiceProvider> 提供给 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> 构造函数的类应将此对象作为类的实现返回 <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> 。

- <xref:System.ComponentModel.Design.IComponentChangeService>

   可以保证使用 Visual Studio 设计宿主提供的默认值的设计器 <xref:System.ComponentModel.Design.DesignSurface> 具有类的默认实现 <xref:System.ComponentModel.Design.IComponentChangeService> 。

<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>如果以下情况，实现基于的撤消机制的设计器会自动跟踪更改：

- 通过对象进行属性更改 <xref:System.ComponentModel.TypeDescriptor> 。

- <xref:System.ComponentModel.Design.IComponentChangeService> 提交可撤消的更改时，将手动生成事件。

- 对设计器的修改是在的上下文中创建的 <xref:System.ComponentModel.Design.DesignerTransaction> 。

- 设计器选择使用由的实现提供的标准撤消单元 <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> 或从派生的 Visual Studio 特定实现来显式创建撤消单元， <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> 同时还提供和的实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> 。

## <a name="see-also"></a>请参阅

- <xref:System.ComponentModel.Design.UndoEngine>
- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>
- [扩展设计时支持](/previous-versions/37899azc(v=vs.140))
