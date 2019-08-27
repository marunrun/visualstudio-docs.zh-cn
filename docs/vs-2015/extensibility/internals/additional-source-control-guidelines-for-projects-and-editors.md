---
title: 项目和编辑器的其他源代码管理指南 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 376b297e94cc8e5f429254bdc981aea994b27130
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203831"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>项目和编辑器的其他源代码管理指南
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

有大量的项目和编辑器应遵循为支持源代码管理的准则。  
  
## <a name="guidelines"></a>准则  
 你的项目或编辑器还应执行以下操作来支持源代码管理：  
  
|区域|项目|编辑器|详细信息|  
|----------|-------------|------------|-------------|  
|文件的私有副本|X||环境支持文件的私有的副本。 也就是说，在项目中登记每个人都有他/她自己的私有副本，在该项目中的文件。|  
|ANSI/Unicode 暂留|X|X|如果您编写的持久性代码，因为大多数源代码管理程序目前不支持 Unicode 保留中的 ANSI 格式的文件。|  
|枚举的文件|X||项目必须包含在其中的所有文件的特定列表，并且必须能要枚举的文件使用的列表<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>(VSH_PROPID_First_Child/Next_Sibling)。 项目还应公开的项名称，通过其<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A>实现和支持名称查找 （包括特殊文件） 通过其<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>实现。|  
|文本格式|X|X|如果可能，文件应以文本格式，以支持不同版本的合并。 不是文本格式的文件不能与其他版本的文件更高版本上合并。 首选的文本格式为 XML。|  
|基于引用的|X||在源代码管理中轻松地支持基于引用的项目。 但是，基于目录的项目也受源代码管理，只要项目可以生成按需，而不考虑这些文件是否存在于磁盘上其文件的列表。 在从源代码管理打开项目，项目文件关闭之前其任何文件的第一个。|  
|保留在可预知的顺序中的对象和属性|X|X|中的文件保存在可预测的顺序，如字母顺序排列，以便合并。|  
|重新加载|X|X|当磁盘上文件更改时，你的编辑器必须能够重新加载它。 如果你参加在源代码管理中，环境将重新加载数据，通过调用你<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A>实现。 签出发生在调用 IVsQueryEditQuerySave 时最困难的重新加载情况是::<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>和正在处理的信息。 但是，在重新加载代码必须能够在此情况下运行。<br /><br /> 环境会自动重新加载项目文件。 但是，一个项目必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>如果有嵌套层次结构以支持重新加载嵌套项目文件。|  
  
## <a name="see-also"></a>请参阅  
 [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
