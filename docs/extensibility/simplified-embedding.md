---
title: 简化的嵌入 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b9bc9619ae1ed75aed3656ff014296f7c7d88fa0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700075"
---
# <a name="simplified-embedding"></a>简化的嵌入
如果在编辑器的文档视图对象的父级为 (即成为) 的子级，则在编辑器中启用简化嵌入， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 实现接口以处理其窗口命令。 简化的嵌入编辑器无法承载活动控件。 下图显示了用于创建具有简化嵌入的编辑器的对象。

 ![简化的嵌入编辑器图形](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor") 具有简化嵌入的编辑器

> [!NOTE]
> 在此图中的对象中，只 `CYourEditorFactory` 需要对象来创建基于文件的标准编辑器。 如果你正在创建自定义编辑器，则不需要实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> ，因为你的编辑器可能具有自己的专用持久性机制。 但对于非自定义编辑器，必须这样做。

 为创建具有简化嵌入的编辑器而实现的所有接口都包含在 `CYourEditorDocument` 对象中。 但是，若要支持文档数据的多个视图，请将接口拆分为单独的数据并查看对象，如下表所示。

|接口|接口的位置|使用|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|查看|提供与父窗口的连接。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|查看|处理命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|查看|启用状态栏更新。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|查看|启用 **工具箱** 项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|数据|当文件发生更改时发送通知。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|数据|为文件类型启用 "另存为" 功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|数据|实现文档持久性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|数据|允许禁止显示文件更改事件，如重新加载触发。|
