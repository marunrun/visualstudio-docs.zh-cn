---
title: 使用旧 API 访问文本层 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text layers
ms.assetid: 2258fcdd-38d1-479d-b8f8-1d4e6525f72c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 975e8624a6ffbfe0c5ae7544f2b978487465e34e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148025"
---
# <a name="accessing-text-layers-by-using-the-legacy-api"></a>使用旧版 API 访问文本层
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本层通常封装文本布局的某个方面。 例如，"函数即时间" 层在包含脱字号 (文本插入点) 的函数之前和之后隐藏文本。  
  
 文本层位于缓冲区和视图之间，并修改视图查看缓冲区内容的方式。  
  
## <a name="text-layer-information"></a>文本层信息  
 以下列表描述文本层在中的工作方式 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ：  
  
- 可以使用语法着色和标记来装饰文本层中的文本。  
  
- 当前无法实现自己的层。  
  
- 层公开 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer> ，它派生自 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> 。 文本缓冲区本身也作为层实现，这使视图可以通过基础层处理以多元方式。  
  
- 视图和缓冲区之间可以有任意数量的层。 每个层仅处理其下的层，并且该视图很大程度上依赖于最顶层的层。  (该视图具有有关缓冲区的某些信息。 )   
  
- 层只能影响其下的层。 它不会影响超出源标准事件的层级。  
  
- 在编辑器中，隐藏文本、合成文本和自动换行都作为层实现。 您可以实现隐藏和合成文本，而无需直接与层交互。 有关详细信息，请参阅 [旧版语言服务中的大纲显示](../extensibility/internals/outlining-in-a-legacy-language-service.md) 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSyntheticTextSession> 。  
  
- 每个文本层都有自己的本地坐标系统，该系统通过 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer> 接口公开。 例如，行环绕层可能包含两行，而基础文本缓冲区可能只包含一行。  
  
- 视图通过接口与层通信 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView> 。 使用此接口可协调视图坐标和缓冲区坐标。  
  
- 任何层（如产生文本的合成文本层）都必须提供的本地实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CreateTrackingPoint%2A> 。  
  
- 除此之外 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer> ，文本层还必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 并激发接口中的事件 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents> 。  
  
## <a name="see-also"></a>另请参阅  
 [自定义编辑器中的语法着色](../extensibility/syntax-coloring-in-custom-editors.md)   
 [将文本标记与旧版 API 一起使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [使用旧版 API 自定义编辑器控件和菜单](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md)
