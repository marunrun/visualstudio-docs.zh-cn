---
title: 查询编辑查询保存（源代码管理 VSPackage） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be12297bdaeb112d7421b02da1153ed62d6d14f8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724775"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>查询编辑查询保存（源代码管理 VSPackage）
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 编辑器可以广播查询编辑查询保存（QEQS）事件。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理存根实现 QEQS 服务，使其成为 QEQS 事件的接收方。 然后，将这些事件委托给当前处于活动状态的源代码管理 VSPackage。 活动源代码管理 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 及其方法。 通常，在首次编辑文档之前和在保存文档之前立即调用 `IVsQueryEditQuerySave2` 接口的方法。

## <a name="queryeditquerysave-events"></a>QueryEditQuerySave 事件
 源代码管理 VSPackage 必须通过实现 `IVsQueryEditQuerySave2` 接口和所需的方法来处理 QEQS 事件。 下面简要说明了 VSPackage 必须实现的两种方法。 实际实现必须符合源代码管理模型的逻辑。

### <a name="queryeditfiles-method"></a>QueryEditFiles 方法
 当任何项目或编辑器要修改文件时，都将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>。 理想情况下，在修改文件和保存文件*之前*调用此方法。 调用时，`IVsQueryEditQuerySave2::QueryEditFiles` 方法会检查给定的文件是否受源代码管理，是否需要签出这些文件以及是否可以重新加载它们。 如果情况使文件无法编辑，`IVsQueryEditQuerySave2::QueryEditFiles` 方法会告知调用程序取消编辑。 调用方还可以指定调用模式。 在 "无提示" 模式下，此方法仅在不会导致 UI 出现时才采取措施。 如果无法避免 UI，则必须返回一个标志来指示问题。

 此方法的行为以事务性方式进行：也就是说，如果对一个文件取消了编辑，则会取消对所有文件的编辑。 相反，如果允许编辑，则所有文件都允许使用。 如果此方法允许对一组给定的文件进行一次编辑，则必须始终允许对同一组文件的后续调用进行编辑。 如果关闭、保存并重新加载文件，则允许编辑循环将继续;直到它们的属性（属性）更改;或直到源代码管理包更改。 实现 `IVsQueryEditQuerySave2::QueryEditFiles` 方法时要考虑的情况包括多个文件、特殊文件、从用户取消和内存中编辑。

### <a name="querysavefiles-method"></a>QuerySaveFiles 方法
 当任何项目或编辑器需要保存一组文件时，将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>。 调用时，`IVsQueryEditQuerySave2::QuerySaveFiles` 方法会检查给定的文件是否是只读的，以及它们是否受源代码管理。 如果需要签出文件，则会将调用委托给源代码管理包。 如果情况阻止保存文件，`IVsQueryEditQuerySave2::QuerySaveFiles` 方法必须告知编辑器取消保存。 与 `IVsQueryEditQuerySave2::QueryEditFiles` 方法一样，调用方可以指定调用模式。 在 "无提示" 模式下，此方法仅在不会导致 UI 出现时才采取措施。 如果无法避免 UI，则必须返回一个标志来指示问题。

 此方法必须采用事务性方式：也就是说，如果对一个文件取消了保存，则会取消所有文件的保存。 相反，如果允许保存，则必须对所有文件都允许该保存。 与 `IVsQueryEditQuerySave2::QueryEditFiles` 方法一样，实现 `IVsQueryEditQuerySave2::QuerySaveFiles` 方法时要考虑的情况包括多个文件、特殊文件、取消用户以及内存中编辑。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>