---
title: 源控件的设计决策 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 89d125dc52340e8528ee9692d5de00784632e6f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187888"
---
# <a name="source-control-design-decisions"></a>源代码管理设计决策
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

实现源代码管理时应考虑以下设计决策的项目。  
  
## <a name="will-information-be-shared-or-private"></a>将信息为共享或专用？  
 可在最重要的设计决策是哪些信息是可共享，什么是私有。 例如，共享的项目文件的列表，但在此列表中的文件，某些用户可能想要将专用文件。 共享的编译器设置，但通常专用启动项目。 设置为完全共享、 共享的替代方法，或完全专用。 根据设计，专用项，如解决方案用户选项 (.suo) 文件未签入到[!INCLUDE[vsvss](../../includes/vsvss-md.md)]。 请务必将任何私人信息存储在.suo 文件或创建，例如，特定的专用文件等专用文件。 csproj.user 文件对于 Visual C# 或。 对于 Visual Basic vbproj.user 文件。  
  
 这一决定并不包含一切可基于项的项。  
  
## <a name="will-the-project-include-special-files"></a>将该项目包括特殊文件？  
 另一个重要设计决策是项目结构是否使用特殊文件。 特殊文件是隐藏的文件的基础是显示在解决方案资源管理器并在签入和签出对话框的文件。 如果使用的特殊文件，请遵循以下准则：  
  
1. 不要将特殊文件关联的项目根节点-也就是说，与项目文件本身。 你的项目文件必须是单个文件。  
  
2. 当添加、 移除或重命名在项目中，相应特殊文件<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>必须设置了标志，指示这些文件是特殊文件不再触发事件。 这些事件通过调用适当的项目的响应中的环境称为<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>方法。  
  
3. 当你的项目或编辑器调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>文件，请与该文件相关联的特殊文件未自动签出。传递以及父文件中的特殊文件。 环境将检测中传递的所有文件之间的关系，并相应地隐藏签出 UI 中的特殊文件。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
