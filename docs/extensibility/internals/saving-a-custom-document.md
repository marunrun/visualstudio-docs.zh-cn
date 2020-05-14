---
title: 保存自定义文档 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f04d588b4becfa778407269849032ea8ec56fb3f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705614"
---
# <a name="saving-a-custom-document"></a>保存自定义文档
环境处理 **"保存**"、**保存为**"和 **"保存所有命令**"。 当用户单击"**保存**"、"**保存为**"**或"全部保存**"到 **"文件**"菜单或关闭解决方案，导致"全部保存"时，将发生以下过程。

 ![客户编辑器保存](../../extensibility/internals/media/private.gif "Private")为自定义编辑器保存、保存为和保存所有命令处理

 此过程在以下步骤中进行了详细说明：

1. 对于 **"保存****和保存为"** 命令，环境使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务来确定活动文档窗口，从而确定哪些项应保存。 知道活动文档窗口后，环境在正在运行的文档表中查找文档的层次结构指针和项标识符 （itemID）。 有关详细信息，请参阅[运行文档表](../../extensibility/internals/running-document-table.md)。

     对于"全部保存"命令，环境使用正在运行的文档表中的信息编译要保存的所有项的列表。

2. 当解决方案收到呼叫时<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>，它会通过所选项集（即<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>服务公开的多个选择）进行遍接。

3. 在所选内容中的每个项上，解决方案使用层次结构指针调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A>方法来确定是否应启用"保存菜单"命令。 如果一个或多个项目脏，则启用"保存"命令。 如果层次结构使用标准编辑器，则层次结构通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A>方法将查询脏状态的层次结构委托给编辑器。

4. 在每个脏的选定项上，解决方案使用层次结构指针在适当的层次结构上调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A>方法。

     对于自定义编辑器，文档数据对象和项目之间的通信是私有的。 因此，在这两个对象之间处理任何特殊的持久性问题。

    > [!NOTE]
    > 如果实现自己的持久性，请确保调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>方法以节省时间。 此方法检查以确保保存文件是安全的（例如，该文件不是只读的）。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
