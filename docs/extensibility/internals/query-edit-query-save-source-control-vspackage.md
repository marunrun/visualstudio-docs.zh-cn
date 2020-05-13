---
title: 查询编辑查询保存（源控制 VS 包） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c09ac0cb4f51b8f2484b95d403ff6d0445631479
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705960"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>查询编辑查询保存（源代码管理 VSPackage）
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]编辑人员可以广播查询编辑查询保存 （QEQS） 事件。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理存根实现 QEQS 服务，因此它是 QEQS 事件的接收者。 然后，这些事件将委派给当前活动的源代码管理 VSPackage。 活动源控件 VSPackage 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>及其方法。 `IVsQueryEditQuerySave2`接口的方法通常在文档首次编辑之前和文档保存之前立即调用。

## <a name="queryeditquerysave-events"></a>查询编辑保存事件
 源代码管理 VSPackage 必须通过实现`IVsQueryEditQuerySave2`接口和必要的方法来处理 QEQS 事件。 以下是 VSPackage 必须至少实现的两种方法的简要说明。 实际实现必须符合源代码管理模型的逻辑。

### <a name="queryeditfiles-method"></a>查询编辑文件方法
 当<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>任何项目或编辑器要修改文件时，将调用 。 理想情况下，在修改文件并保存文件*之前*调用此方法。 调用时，`IVsQueryEditQuerySave2::QueryEditFiles`该方法将检查给定文件是否处于源代码管理之下，是否需要签出这些文件，以及是否可以重新加载这些文件。 如果情况阻止文件可编辑，`IVsQueryEditQuerySave2::QueryEditFiles`则该方法会告诉调用程序取消编辑。 调用方也可以指定调用模式。 在"静默"模式下，此方法仅在它不导致出现任何 UI 时才执行操作。 如果 UI 不可避免，则必须返回标志以指示问题。

 该方法以事务方式运行;也就是说，如果单个文件上取消编辑，则取消所有文件的编辑。 相反，如果允许编辑，则允许对所有文件进行编辑。 如果此方法允许对一组给定的文件进行编辑一次，则必须始终允许对同一组文件的后续调用进行编辑。 允许编辑循环将继续，直到关闭、保存和重新加载文件;直到他们的属性（属性）发生变化;或直到源控制包被更改。 实现`IVsQueryEditQuerySave2::QueryEditFiles`该方法时需要考虑的情况包括多个文件、特殊文件、用户取消和内存内编辑。

### <a name="querysavefiles-method"></a>查询保存文件方法
 当<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>任何项目或编辑器需要保存一组文件时，将调用 。 调用时，`IVsQueryEditQuerySave2::QuerySaveFiles`该方法将检查给定文件是否为只读文件，以及这些文件是否处于源代码管理之下。 如果需要签出文件，则调用将委派给源代码管理包。 如果情况阻止保存文件，`IVsQueryEditQuerySave2::QuerySaveFiles`则方法必须告诉编辑器取消保存。 与 方法`IVsQueryEditQuerySave2::QueryEditFiles`一样，调用方可以指定调用模式。 在"静默"模式下，此方法仅在它不导致出现任何 UI 时才执行操作。 如果 UI 不可避免，则必须返回标志以指示问题。

 此方法必须以事务方式运行;也就是说，如果单个文件中的保存被取消，则所有文件的保存将被取消。 相反，如果允许保存，则必须允许所有文件进行保存。 与该方法一`IVsQueryEditQuerySave2::QueryEditFiles`样，在实现`IVsQueryEditQuerySave2::QuerySaveFiles`该方法时需要考虑的案例包括多个文件、特殊文件、用户取消和内存内编辑。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
