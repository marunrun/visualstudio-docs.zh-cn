---
title: 项目和编辑的其他源代码管理指南 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 181f6c10ff7ce95cd3a37151f117353d1bb47d41
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710107"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>项目和编辑器的其他源代码管理指南
项目和编辑应遵守许多准则来支持源代码管理。

## <a name="guidelines"></a>指南
 您的项目或编辑器还应执行以下操作来支持源代码管理：

|区域|Project|编辑器|详细信息|
|----------|-------------|------------|-------------|
|文件的私人副本|X||环境支持文件的私人副本。 也就是说，在项目中登记的每个人都有自己/她该项目中文件的私人副本。|
|ANSI/Unicode 持久性|X|X|如果编写持久性代码，请在 ANSI 窗体中保留文件，因为大多数源代码控制程序当前不支持 Unicode。|
|枚举文件|X||项目必须包含其中所有文件的特定列表，并且必须能够枚举使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>（VSH_PROPID_First_Child/Next_Sibling）的文件列表。 项目还应通过其<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A>实现公开项目名称，并通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>支持名称查找（包括特殊文件）。|
|文本格式|X|X|如果可能，文件应采用文本格式，以支持合并不同版本。 以后不能将不是文本格式的文件与其他版本的文件合并。 首选文本格式是 XML。|
|基于参考|X||源代码管理中很容易支持基于引用的项目。 但是，只要项目可以按需生成其文件的列表，无论磁盘上是否存在这些文件，源代码管理也会支持基于目录的项目。 从源代码管理打开项目时，项目文件首先在其任何文件之前被下拉。|
|以可预测的顺序持久化对象和属性|X|X|以可预测的顺序（如字母顺序）保留文件，以方便合并。|
|重新加载|X|X|当磁盘上的文件发生更改时，编辑器必须能够重新加载它。 当您参与源代码管理时，环境将通过调用实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>来重新加载数据。 最困难的重新加载案例是在调用 IVsQueryEditQuerySave：<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>和正在处理信息时发生签出时。 但是，重新加载代码必须能够在此情况下运行。<br /><br /> 环境会自动重新加载项目文件。 但是，如果项目具有嵌套<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>层次结构，则必须实现，以支持重新加载嵌套项目文件。|

## <a name="see-also"></a>请参阅
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
