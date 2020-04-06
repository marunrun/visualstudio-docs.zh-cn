---
title: 项目优先级 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a75c1c333d88e1bf5524281bee8b2a683ca6c98e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706422"
---
# <a name="project-priority"></a>项目优先级
项目项通常只是解决方案中一个项目的成员。 因此，IDE 可以轻松地确定用于打开项目的项目。 但是，如果项目是多个项目的成员，IDE 将使用优先级方案来确定打开项目的最佳项目。

 以下列表显示了项目优先级方案：

- IDE 调用解决方案<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A>中每个项目的方法，以确定文档是否是该项目的成员。

- 如果文档是项目的成员，则项目会响应项目根据对该文件的处理所分配的优先级。 例如，语言项目对其语言源文件具有高优先级的响应，但对于未识别的文件类型，响应优先级较低，而这些文件类型不用作其生成过程的一部分。

- 为文档提供自定义、特定于项目的编辑器或设计器的项目也会获得高度优先级。

- 枚<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>举提供文档优先级值。

- 指定最高优先级的项目将指定打开文档的上下文。 如果两个项目返回相等的优先级值，则首选活动项目。 如果解决方案中没有项目响应可以打开文档，IDE 会将文档放入"杂项文件"项目中。 有关详细信息，请参阅[杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)。

## <a name="see-also"></a>请参阅
- [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)
- [如何：打开开放文档的编辑器](../../extensibility/how-to-open-editors-for-open-documents.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
