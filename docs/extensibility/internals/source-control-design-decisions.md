---
title: 源代码管理设计决策 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705246"
---
# <a name="source-control-design-decisions"></a>源代码管理设计决策
实现源代码管理时，应考虑以下设计决策。

## <a name="will-information-be-shared-or-private"></a>信息是共享还是专用？
 你可以进行的最重要的设计决策是可共享的信息，以及什么是私有的。 例如，项目的文件列表是共享的，但在此文件列表中，某些用户可能想要拥有专用文件。 编译器设置是共享的，但启动项目通常是专用的。 设置是纯粹共享的，使用重写共享，或纯粹是专用的。 按照设计，将不签入私有项（如解决方案用户选项 ( .suo) 文件） [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] 。 请确保在专用文件（如 .suo 文件）或创建的特定专用文件（例如，用于 Visual c # 的 .csproj 文件或 Visual Basic 的 .vbproj 文件）中存储任何专用信息。

 此决定并不完全相同，并可逐个项进行。

## <a name="will-the-project-include-special-files"></a>该项目是否包含特殊文件？
 另一个重要的设计决策是您的项目结构是否使用特殊文件。 特殊文件是在 "签入" 和 "签出" 对话框中以解决方案资源管理器显示的文件为基础的隐藏文件。 如果使用特殊文件，请遵循以下准则：

1. 不要将特殊文件与项目根节点相关联，即项目文件本身。 你的项目文件必须是单个文件。

2. 当在项目中添加、删除或重命名特殊文件时， <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 必须使用指示文件是特殊文件的标志设置来激发相应的事件。 这些事件由环境调用，以响应调用相应方法的项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 。

3. 当项目或编辑器调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 某个文件时，与该文件关联的特殊文件不会自动签出。将特殊文件与父文件一起传递。 环境将检测传入的所有文件之间的关系，并在签出 UI 中适当地隐藏特殊文件。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
