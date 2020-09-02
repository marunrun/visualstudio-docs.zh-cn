---
title: 就地激活 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - in-place view activation
ms.assetid: 7d316945-06e0-4d8e-ba3a-0ef96fc75399
caps.latest.revision: 26
manager: jillfra
ms.openlocfilehash: 192274d087731f68cb7e01c1da20e80cbfef0360
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "64802923"
---
# <a name="in-place-activation"></a>就地激活
如果你的编辑器视图托管了 ActiveX 或其他活动控件，则必须使用就地激活模型将编辑器视图实现为 ActiveX 控件或活动文档数据对象。  
  
## <a name="support-for-menus-toolbars-and-commands"></a>支持菜单、工具栏和命令  
 Visual Studio 允许你的编辑器视图使用 IDE 的菜单和工具栏。 这些扩展被称为 *OLE 就地组件*。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager>。  
  
 如果实现了 ActiveX 控件，则可以托管其他嵌入对象。 如果你实现了文档数据对象，窗口框架将限制你使用 ActiveX 控件的能力。  
  
> [!NOTE]
> <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument> 和 <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocumentView> 接口允许分离数据与视图。 但是，Visual Studio 不支持此功能，并且这些接口仅用于表示文档视图对象。  
  
 使用 <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> 服务的编辑器可以通过调用由 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> 服务实现的 <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> 接口的方法来提供菜单、工具栏和命令的集成。 编辑器还可以提供其他 Visual Studio 功能，例如，选择跟踪和撤消管理。 有关详细信息，请参阅 [创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)。  
  
## <a name="objects-and-interfaces-used"></a>使用的对象和接口  
 下图中显示了用于创建就地激活的对象。  
  
 ![在&#45;放置激活编辑器](../misc/media/vsinplaceactivationeditor.gif "vsInPlaceActivationEditor")  
就地激活编辑器  
  
> [!NOTE]
> 此绘图的对象中，仅 `CYourEditorFactory` 对象是创建标准编辑器必需的对象。 如果要创建自定义编辑器，不必实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> ，因为你的编辑器可能具有自己的专用持久性机制。 有关详细信息，请参阅 [创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)。  
  
 为了创建就地激活编辑器而实现的所有接口都显示在单个 `CYourEditorDocument` 对象上，但此配置仅支持文档数据的单一视图。 有关支持文档数据的多个视图的详细信息，请参阅 [Supporting Multiple Document Views](../extensibility/supporting-multiple-document-views.md)。  
  
|接口|对象的类型|使用|  
|---------------|--------------------|---------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>|查看|通过使用 <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> 服务，使就地 VSPackage 对象能够作为完全集成的 IDE 组件来工作。 此服务将对象的菜单、工具栏和命令集成到 IDE 中，并发出状态更改通知。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>|查看|嵌入对象向其容器提供基本功能并与该容器通信的主要手段。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>|查看|管理就地对象的激活和停用，并确定应为可见的就地对象数目。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceObject>|查看|为就地对象、关联应用程序的最外侧框架窗口，以及包含嵌入对象的应用程序中的文档窗口之间的通信提供一个直接的通道。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument>|查看|实现 ActiveX 对象。 请注意，IDE 中未使用分隔文档数据与视图的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleDocument> 和 `T:Microsoft.VisualStudio.OLE.Interop.IOleDocumentView` 方法。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|视图/数据|使文档数据对象和/或文档视图对象能够参与命令处理。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|查看|启用状态栏更新。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|查看|实现向工具箱添加项。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|数据|向已编辑的文件发送更改通知。 （此接口是可选的。）|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|数据|用于为某一文件类型启用“另存为”功能。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|数据|实现文档持久性。 对于只读文件，调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SetDocDataReadOnly%2A> 以提供“锁状”图标来表示只读文件。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|数据|确定是否应忽略对文档数据的更改。|