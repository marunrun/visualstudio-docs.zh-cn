---
title: 保存自定义文档 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705614"
---
# <a name="saving-a-custom-document"></a>保存自定义文档
环境处理 " **保存**"、" **另存为**" 和 " **保存所有** " 命令。 当用户单击 " **保存**"、" **另存为**" **或 "全部保存** " 或 "全部保存" 在 " **文件** " 菜单上或关闭解决方案时，将会产生以下过程。

 ![客户编辑器保存](../../extensibility/internals/media/private.gif "专用") 为自定义编辑器保存、保存并保存所有命令处理

 以下步骤详细说明了此过程：

1. 对于 " **保存** " 和 " **另存为** " 命令，环境使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务来确定活动文档窗口，并因此应保存哪些项。 已知活动文档窗口后，环境将查找正在运行的文档表中文档 (itemID) 的层次结构指针和项标识符。 有关详细信息，请参阅 [运行文档表](../../extensibility/internals/running-document-table.md)。

     对于 "全部保存" 命令，环境使用正在运行的文档表中的信息来编译要保存的所有项的列表。

2. 当解决方案接收到 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 调用时，它将循环访问所选项集， (即服务公开的多个选择 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>) 。

3. 对于选定内容中的每一项，解决方案都使用层次结构指针来调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> 方法，以确定是否应启用 "保存" 菜单命令。 如果一个或多个项目已被更新，则启用 Save 命令。 如果层次结构使用标准编辑器，则层次结构会通过调用方法，将查询的脏状态委托给编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> 。

4. 在每个未更新的选定项上，解决方案使用层次结构指针对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 适当的层次结构调用方法。

     对于自定义编辑器，文档数据对象与项目之间的通信是私有的。 因此，在这两个对象之间处理任何特殊的持久性问题。

    > [!NOTE]
    > 如果实现自己的持久性，请确保调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> 方法来节省时间。 此方法将进行检查以确保保存文件 (例如，文件不是只读的) 。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
