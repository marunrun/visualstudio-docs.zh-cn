---
title: 简化的嵌入 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700075"
---
# <a name="simplified-embedding"></a>简化的嵌入
当其文档视图对象父级为 （即 创建 子 对象）[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>在编辑器中启用简化的嵌入，并且接口被实现以处理其窗口命令。 简化的嵌入编辑器无法承载活动控件。 用于使用简化嵌入创建编辑器的对象如下图所示。

 ![简化的嵌入编辑器图形](../extensibility/media/vssimplifiedembeddingeditor.gif "vs 简化的嵌入编辑器")具有简化嵌入的编辑器

> [!NOTE]
> 在此图中的对象中，只需创建`CYourEditorFactory`基于文件的标准编辑器即可创建对象。 如果要创建自定义编辑器，则不需要实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>，因为编辑器可能有自己的私有持久性机制。 但是，对于非自定义编辑器，您必须这样做。

 为创建具有简化嵌入的编辑器而实现的所有接口都包含在对象中`CYourEditorDocument`。 但是，要支持文档数据的多个视图，可以将接口拆分为单独的数据，并按照下表所示查看对象。

|接口|接口位置|使用|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|视图|提供与父窗口的连接。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|视图|处理命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|视图|启用状态栏更新。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|视图|启用**工具箱**项目。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|数据|文件更改时发送通知。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|数据|为文件类型启用"保存为"功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|数据|实现文档持久性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|数据|允许抑制文件更改事件，如重新加载触发。|
