---
title: 查询编辑查询保存 (源代码管理 VSPackage) |Microsoft Docs
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
ms.openlocfilehash: d3bffdac79a9f4274fbd6465c33e8659caf9d1f6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341454"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>查询编辑查询保存（源代码管理 VSPackage）
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 编辑器可以广播保存查询编辑查询 (QEQS) 事件。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源存根 （stub） 实现 QEQS 服务，以便它 QEQS 事件接收方。 然后，这些事件被委托给当前处于活动状态的源代码管理 VSPackage。 活动的源代码管理 VSPackage 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>及其方法。 方法`IVsQueryEditQuerySave2`接口通常称为第一次和保存文档之前编辑文档之前。

## <a name="queryeditquerysave-events"></a>QueryEditQuerySave 事件
 源代码管理 VSPackage 必须通过实现来处理 QEQS 事件`IVsQueryEditQuerySave2`接口和必需的方法。 下面是 VSPackage 必须实现至少两个方法的简要说明。 根据源控件模型的逻辑必须是实际的实现。

### <a name="queryeditfiles-method"></a>QueryEditFiles 方法
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>任何项目或编辑器中想要修改的文件时调用。 理想情况下，此方法称为*之前*修改该文件并保存文件时。 调用时，`IVsQueryEditQuerySave2::QueryEditFiles`方法检查给定的文件是否受源代码管理，他们是否需要签出，以及是否重载。 如果情况下防止文件被编辑，`IVsQueryEditQuerySave2::QueryEditFiles`方法告诉调用程序来取消编辑。 还有可能为使调用方指定的调用模式。 在"静默"模式下，此方法采用操作才不会导致出现任何 UI。 如果 UI 是不可避免的必须返回一个标志以指示该问题。

 该方法的行为以事务的方式;也就是说，如果单个文件取消了编辑，则编辑将被取消的所有文件。 相反，如果允许编辑，则允许使用的所有文件。 如果此方法允许为一组给定的文件一次编辑，必须始终允许编辑同一组文件的后续调用。 允许编辑循环继续直到关闭、 保存，并重新加载; 文件直到更改及其属性 （属性）;或更改源代码管理包之前。 在实现时需要考虑的情况下`IVsQueryEditQuerySave2::QueryEditFiles`方法包括多个文件，特殊文件，取消从用户，并在内存中编辑。

### <a name="querysavefiles-method"></a>QuerySaveFiles 方法
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>保存一组文件时所需要的任何项目或编辑器时调用。 调用时，`IVsQueryEditQuerySave2::QuerySaveFiles`方法检查如果给定的文件是只读的无论它们是在源代码管理下。 如果需要签出文件，在调用委托给源代码管理包。 如果情况下防止文件被保存，`IVsQueryEditQuerySave2::QuerySaveFiles`方法必须告知编辑器取消保存。 与使用`IVsQueryEditQuerySave2::QueryEditFiles`方法，就可以为指定的调用模式使调用方。 在"静默"模式下，此方法采用操作才不会导致出现任何 UI。 如果 UI 是不可避免的必须返回一个标志以指示该问题。

 此方法必须在事务的方式; 中的行为也就是说，如果单个文件取消了保存，则保存取消所有文件。 相反，如果允许保存，则它必须允许所有文件。 如同`IVsQueryEditQuerySave2::QueryEditFiles`方法中，在实现时需要考虑的情况下`IVsQueryEditQuerySave2::QuerySaveFiles`方法包括多个文件，特殊文件，取消从用户，并在内存中编辑。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>