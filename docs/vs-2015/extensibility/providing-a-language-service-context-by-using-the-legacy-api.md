---
title: 使用旧版 API 提供语言服务上下文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language service context
ms.assetid: daa2df22-9181-4bad-b007-a7d40302bce1
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4471b71b612008ba7d0733c92286415cd3c3f6b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193865"
---
# <a name="providing-a-language-service-context-by-using-the-legacy-api"></a>使用旧版 API 提供语言服务上下文
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

语言服务有两个选项可用于使用核心编辑器提供用户上下文 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ：提供文本标记上下文，或提供所有用户上下文。 下面概述了二者之间的差异。  
  
 有关为连接到您自己的编辑器的语言服务提供上下文的详细信息，请参阅 [如何：为编辑器提供上下文](../extensibility/how-to-provide-context-for-editors.md)。  
  
## <a name="provide-text-marker-context-to-the-editor"></a>向编辑器提供文本标记上下文  
 若要为核心编辑器中的文本标记所指示的编译器错误提供上下文 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，请实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> 接口。 在此方案中，语言服务仅在光标位于文本标记上时提供上下文。 这允许编辑器在不具有属性的 **动态帮助** 窗口中提供关键字。  
  
## <a name="provide-all-user-context-to-the-editor"></a>向编辑器提供所有用户上下文  
 如果正在创建语言服务，并且使用的是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 核心编辑器，则可以实现接口，为 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> 语言服务提供上下文。  
  
 对于的实现 `IVsLanguageContextProvider` ， (集合) 的上下文包附加到编辑器，该编辑器负责更新上下文包。 当 " **动态帮助** " 窗口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.Update%2A> 在此上下文包处于空闲状态时调用接口时，上下文包将查询编辑器以获取更新。 然后，该编辑器通知语言服务它应更新编辑器，并传递指向上下文包的指针。 这是通过 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider.UpdateLanguageContext%2A> 将方法从编辑器调用到语言服务来完成的。 使用指向上下文包的指针，语言服务现在可以添加和删除属性和关键字。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>。  
  
 可以通过两种不同的方法实现 `IVsLanguageContextProvider` ：  
  
- 向上下文包提供关键字  
  
   调用编辑器以更新上下文包时，传递相应的关键字和特性，然后返回 `S_OK` 。 此返回值指示编辑器保留关键字和属性上下文，而不是向上下文包提供光标处的关键字。  
  
- 从游标的关键字中获取关键字  
  
   调用编辑器以更新上下文包时，传递适当的属性，然后返回 `E_FAIL` 。 此返回值指示编辑器在上下文包中保留属性，但在游标中用关键字更新上下文包。  
  
  下图演示了如何为实现的语言服务提供上下文 `IVsLanguageContextProvider` 。  
  
  ![LangServiceImplementation2 图](../extensibility/media/vslanguageservice2.gif "vsLanguageService2")  
  语言服务的上下文  
  
  如图中所示， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 核心文本编辑器附加了上下文包。 此上下文包指向三个单独的子上下文包：语言服务、默认编辑器和文本标记。 如果实现了接口，则语言服务和文本标记子上下文包包含语言服务的属性和关键字 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> ，如果实现了接口，则包含文本标记 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> 。 如果未实现这些接口中的任何一个，则编辑器将在默认编辑器分上下文包的光标处提供关键字的上下文。  
  
## <a name="context-guidelines-for-editors-and-designers"></a>编辑器和设计器的上下文准则  
 设计器和编辑器必须提供编辑器或设计器窗口的常规关键字。 这样做的目的是，当用户按 F1 时，将为设计器或编辑器显示一般的、但适当的帮助主题。 除了此外，编辑器还必须在光标处提供当前关键字，或者根据当前选择提供键术语。 这样做是为了确保当用户按 F1 时，将显示指向或所选的文本或 UI 元素的帮助主题。 设计器为设计器中选定的项提供上下文，如窗体上的按钮。 编辑器和设计器还必须连接到 [旧版语言服务基础](../extensibility/internals/legacy-language-service-essentials.md)中所述的语言服务。
