---
title: 源代码管理设计决策 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c36bb2b50a72a52aeaeb7712f4ed711845b5e6d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705246"
---
# <a name="source-control-design-decisions"></a>源代码管理设计决策
在实现源代码管理时，应考虑以下设计决策。

## <a name="will-information-be-shared-or-private"></a>信息是共享还是私有？
 您可以做出的最重要的设计决策是哪些信息是可共享的，什么是私有的。 例如，项目的文件列表是共享的，但在此文件列表中，某些用户可能希望具有私有文件。 编译器设置是共享的，但启动项目通常是私有的。 设置是纯共享的、与重写共享的，或者纯粹是私有的。 根据设计，私有项目（如解决方案用户选项 （.suo） 文件）不会签入[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]。 请务必将任何私有信息存储在私有文件（如 .suo 文件）或您创建的特定私有文件（例如，Visual C# 的 .csproj.user 文件）或 Visual Basic 的 .vbproj.user 文件中。

 此决定并非包罗万象，可以逐项做出。

## <a name="will-the-project-include-special-files"></a>该项目将包括特殊文件吗？
 另一个重要的设计决策是项目结构是否使用特殊文件。 特殊文件是隐藏文件，这些文件是解决方案资源管理器和签入和签出对话框中可见的文件的隐藏文件。 如果您使用特殊文件，请遵循以下准则：

1. 不要将特殊文件与项目根节点（即项目文件本身）相关联。 项目文件必须是单个文件。

2. 在项目中添加、删除或重命名特殊文件时，必须使用指示文件为特殊<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>文件的标志集触发相应的事件。 这些事件由环境调用，以响应调用相应<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>方法的项目。

3. 当项目或编辑器调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>文件时，与该文件关联的特殊文件不会自动签出。将特殊文件与父文件一起传递。 环境将检测传入的所有文件之间的关系，并适当隐藏签出 UI 中的特殊文件。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
