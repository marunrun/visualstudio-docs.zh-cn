---
title: 简化的嵌入 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c77c7f19ff677ddbe8339c88ef3ea46953e23b7d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332077"
---
# <a name="simplified-embedding"></a>简化的嵌入
当其文档视图对象的父级 （即，做出的子级） 简化的嵌入在编辑器中启用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，和<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>接口实现以处理其窗口命令。 简化的嵌入编辑器不能托管活动控件。 在下图显示用于创建编辑器具有简化的嵌入的对象。

 ![简化的嵌入式编辑器图形](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor")具有简化的嵌入编辑器

> [!NOTE]
> 在此图中，仅对象的`CYourEditorFactory`创建标准的基于文件的编辑器所需的对象。 如果要创建自定义编辑器，不需要实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>，因为你的编辑器可能具有其自己的专用持久性机制。 为非自定义编辑器，但是，则必须这样做。

 中包含所有接口实现以创建具有简化的嵌入编辑器`CYourEditorDocument`对象。 但是，若要支持文档数据的多个视图，拆分到单独的数据与视图对象上的接口下表中所示。

|接口|接口的位置|使用|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|视图|提供连接到父窗口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|视图|处理命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|视图|启用状态栏更新。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|视图|使**工具箱**项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|数据|文件发生更改时，会发送通知。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|数据|启用文件类型的另存为功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|数据|实现文档持久性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|数据|允许文件更改事件，例如触发重新加载禁止的显示。|