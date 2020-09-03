---
title: 查询编辑查询保存 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2ad0cf7c3e1d3269dbe7ebee051cc32e2e8531ef
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148887"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>查询编辑查询保存（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 编辑器可以广播查询编辑查询保存 (QEQS) 事件。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 源代码管理存根实现 QEQS 服务，因此，它是 QEQS 事件的接收方。 然后，将这些事件委托给当前处于活动状态的源代码管理 VSPackage。 活动源代码管理 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 及其方法。 `IVsQueryEditQuerySave2`通常，在首次编辑文档之前和在保存文档之前立即调用接口的方法。  
  
## <a name="queryeditquerysave-events"></a>QueryEditQuerySave 事件  
 源代码管理 VSPackage 必须通过实现 `IVsQueryEditQuerySave2` 接口和所需的方法来处理 QEQS 事件。 下面简要说明了 VSPackage 必须实现的两种方法。 实际实现必须符合源代码管理模型的逻辑。  
  
### <a name="queryeditfiles-method"></a>QueryEditFiles 方法  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>当任何项目或编辑器要修改文件时，都将调用。 理想情况下，在修改文件和保存文件 *之前* 调用此方法。 调用时， `IVsQueryEditQuerySave2::QueryEditFiles` 方法会检查给定的文件是否受源代码管理，是否需要签出这些文件以及是否可以重新加载这些文件。 如果方案阻止对文件进行编辑，则 `IVsQueryEditQuerySave2::QueryEditFiles` 方法会告知调用程序取消编辑。 调用方还可以指定调用模式。 在 "无提示" 模式下，此方法仅在不会导致 UI 出现时才采取措施。 如果无法避免 UI，则必须返回一个标志来指示问题。  
  
 此方法的行为以事务性方式进行：也就是说，如果对一个文件取消了编辑，则会取消对所有文件的编辑。 相反，如果允许编辑，则所有文件都允许使用。 如果此方法允许对一组给定的文件进行一次编辑，则必须始终允许对同一组文件的后续调用进行编辑。 如果关闭、保存并重新加载文件，则允许编辑循环将继续;直到它们的属性 (属性) 更改;或直到源代码管理包更改。 实现方法时要考虑的情况 `IVsQueryEditQuerySave2::QueryEditFiles` 包括多个文件、特殊文件、从用户取消和内存中编辑。  
  
### <a name="querysavefiles-method"></a>QuerySaveFiles 方法  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>当任何项目或编辑器需要保存一组文件时调用。 调用时， `IVsQueryEditQuerySave2::QuerySaveFiles` 方法会检查给定的文件是否是只读的，以及是否受源代码管理。 如果需要签出文件，则会将调用委托给源代码管理包。 如果情况阻止保存文件，则该 `IVsQueryEditQuerySave2::QuerySaveFiles` 方法必须告知编辑器取消保存。 与方法一样 `IVsQueryEditQuerySave2::QueryEditFiles` ，调用方可以指定调用模式。 在 "无提示" 模式下，此方法仅在不会导致 UI 出现时才采取措施。 如果无法避免 UI，则必须返回一个标志来指示问题。  
  
 此方法必须采用事务性方式：也就是说，如果对一个文件取消了保存，则会取消所有文件的保存。 相反，如果允许保存，则必须对所有文件都允许该保存。 与方法一样 `IVsQueryEditQuerySave2::QueryEditFiles` ，实现方法时要考虑的情况 `IVsQueryEditQuerySave2::QuerySaveFiles` 包括多个文件、特殊文件、取消用户和内存中编辑。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
