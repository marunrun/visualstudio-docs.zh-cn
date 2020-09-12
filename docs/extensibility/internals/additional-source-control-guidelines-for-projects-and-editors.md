---
title: 项目和编辑器的源代码管理准则
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 2d1066995537ff6c43a587326c1087b66f79ff52
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037629"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>项目和编辑器的其他源代码管理准则
为了支持源代码管理，项目和编辑人员应遵循一些准则。

## <a name="guidelines"></a>指南
 您的项目或编辑器还应该执行以下操作来支持源代码管理：

|区域|Project|编辑器|详细信息|
|----------|-------------|------------|-------------|
|文件的专用副本|X||环境支持文件的私有副本。 也就是说，在项目中登记的每个人都有其自己的专有文件副本。|
|ANSI/Unicode 持久性|X|X|如果你编写持久性代码，则会将文件保存在 ANSI 形式中，因为大多数源代码管理程序当前不支持 Unicode。|
|枚举文件|X||项目必须包含其中所有文件的特定列表，并且必须能够使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (VSH_PROPID_First_Child/Next_Sibling) 来枚举文件列表。 项目还应通过其实现公开项名称 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A> 并支持名称查找 (包括通过其实现) 的特殊文件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> 。|
|文本格式|X|X|如果可能，文件应为文本格式以支持不同版本的合并。 不是文本格式的文件稍后不能与文件的其他版本合并。 首选文本格式为 XML。|
|基于引用|X||源代码管理中随时支持基于引用的项目。 但是，源代码管理还支持基于目录的项目，只要项目可以按需生成其文件列表，无论这些文件是否存在于磁盘上。 在从源代码管理打开项目时，项目文件首先会在其任何文件之前关闭。|
|以可预测顺序持久保存对象和属性|X|X|以可预测的顺序（如按字母顺序）持久保存文件，以便于合并。|
|重新加载|X|X|当文件在磁盘上更改时，编辑器必须能够重新加载它。 参与源控件时，环境将通过调用你的实现来重新加载数据 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> 。 最难的重载是：在调用 IVsQueryEditQuerySave：： <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 并且正在处理信息时，会发生签出。 但是，在这种情况下，重新加载代码必须能够运行。<br /><br /> 环境会自动重新加载项目文件。 但是， <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> 如果项目具有嵌套层次结构以支持重新加载嵌套的项目文件，则该项目必须实现。|

## <a name="see-also"></a>另请参阅
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
