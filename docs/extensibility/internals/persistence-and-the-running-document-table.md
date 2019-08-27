---
title: 持久性和正在运行文档表 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d80932ab926b7ef26eaef10991e4f5782e81c4b5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328522"
---
# <a name="persistence-and-the-running-document-table"></a>持久性和正在运行的文档表
在中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 中，项目是完全负责管理其项目项，它们为使用该服务，持久性<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>。 文档是在 Visual Studio 环境中的暂留的基本单位。 项目协调在打开、 保存和重命名的文档运行文档表 (RDT) 跟踪所有打开的文档的状态的资源。

## <a name="managing-persistence"></a>管理持久性
 项目通过实现控制环境的持久性服务<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem>接口。 虽然环境永远不会直接询问要保持自身的文档，它会要求所属项目 （或层次结构） 来保存文档。 这使项目及其项目项数据保存到本地文件、 远程文件、 数据库、 一个存储库或其他媒体。

 全局环境负责维护 RDT。 环境负责维护所有打开的窗口的条目和 RDT，这样就可以为它们到中的文档接收特殊的通知，例如，解决方案已关闭时。 此外，RDT 使得要跟踪其对应的节点中的环境**解决方案资源管理器**。 RDT 维护每个打开、 持久对象，其中包括项目文件和项目项的文档的一条记录。

## <a name="see-also"></a>请参阅
- [运行文档表](../../extensibility/internals/running-document-table.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)