---
title: 保存自定义文档 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b90938e44b4227f8aad43542fc99136745a8af4e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318742"
---
# <a name="saving-a-custom-document"></a>保存自定义文档
环境句柄**保存**，**另存为**，并**全部保存**命令。 当用户单击**保存**，**另存为**，**或全部保存**上**文件**菜单或关闭解决方案，从而导致全部保存，以下执行过程。

 ![客户编辑器保存](../../extensibility/internals/media/private.gif "专用")保存、 另存为，并保存所有的命令处理自定义编辑器

 此过程详述以下步骤：

1. 有关**保存**并**另存为**命令，在环境中使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务以确定活动文档窗口，并应因此保存项。 活动文档窗口了解后，在环境中正在运行的 document 表的文档查找的层次结构的指针和项标识符 (itemID)。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。

     为全部保存命令，该环境使用中的信息运行文档表编译要保存的所有项的列表。

2. 当解决方案收到<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>调用时，它会循环访问选定项的集 (即，公开多个选择<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务)。

3. 选定内容中的每个项，该解决方案使用层次结构指针来调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>方法，以确定是否应启用保存菜单命令。 如果一个或多个项是脏的则启用保存命令。 如果在层次结构使用的标准编辑器，然后查询的层次结构委托脏状态设置为编辑器中通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>方法。

4. 已更新的每个选定项，该解决方案使用层次结构指针来调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>适当的层次结构上的方法。

     对于自定义编辑器中，文档数据对象和项目之间的通信是私有的。 因此，任何特殊的持久性问题被处理这两个对象之间。

    > [!NOTE]
    > 如果您实现您自己的持久性，请务必调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>方法来节省时间。 此方法进行检查以确保其安全地保存该文件 （例如，文件不是只读的）。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)