---
title: 持久性和正在运行文档表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2c422ad1735312c82c8dc027c4adf73c1b033685
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196094"
---
# <a name="persistence-and-the-running-document-table"></a>持久性和正在运行的文档表
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 中，项目是完全负责管理其项目项，它们为使用该服务，持久性<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>。 文档是在 Visual Studio 环境中的暂留的基本单位。 项目协调在打开、 保存和重命名的文档运行文档表 (RDT) 跟踪所有打开的文档的状态的资源。  
  
## <a name="managing-persistence"></a>管理持久性  
 项目通过实现控制环境的持久性服务<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem>接口。 虽然环境永远不会直接询问要保持自身的文档，它会要求所属项目 （或层次结构） 来保存文档。 这使项目及其项目项数据保存到本地文件、 远程文件、 数据库、 一个存储库或其他媒体。  
  
 全局环境负责维护 RDT。 环境负责维护所有打开的窗口的条目和 RDT，这样就可以为它们到中的文档接收特殊的通知，例如，解决方案已关闭时。 此外，RDT 使得要跟踪其对应的节点中的环境**解决方案资源管理器**。 RDT 维护每个打开、 持久对象，其中包括项目文件和项目项的文档的一条记录。  
  
## <a name="see-also"></a>请参阅  
 [运行文档表](../../extensibility/internals/running-document-table.md)   
 [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
