---
title: 持久性和正在运行的文档表 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba698f20b83d1a7af42aeca046aa2a8c943838ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706723"
---
# <a name="persistence-and-the-running-document-table"></a>持久性和正在运行的文档表
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 中，项目完全负责管理其项目项的持久性，它们使用服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>完成。 文档是可视化工作室环境中持久性的基本单元。 项目使用正在运行的文档表 （RDT） 协调文档的打开、保存和重命名，这是跟踪所有打开文档状态的资源。

## <a name="managing-persistence"></a>管理持久性
 项目通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem>接口来控制环境的持久性服务。 虽然环境从不直接要求文档持久化，但它要求拥有的项目（或层次结构）保存文档。 这使得项目能够将其项目项数据保存到本地文件、远程文件、数据库、存储库或其他介质中。

 全局环境维护 RDT。 环境维护 RDT 中所有打开的窗口和文档的条目，这使他们能够接收特殊通知，例如关闭解决方案时。 此外，RDT 使环境能够跟踪**其相应的节点在解决方案资源管理器**中。 RDT 维护每个打开的可持久对象一条记录，包括项目文件和项目项目文档。

## <a name="see-also"></a>请参阅
- [运行文档表](../../extensibility/internals/running-document-table.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
