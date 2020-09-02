---
title: 包含的语言 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - contained languages
ms.assetid: b75bbb51-8e42-41b1-bece-09ab0b1f03cc
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0920999eee7460c8bf697e245bae55a3641b8e18
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184276"
---
# <a name="contained-languages"></a>包含的语言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)] 

*包含的语言* 是由其他语言包含的语言。 例如，网页中的 HTML [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 可能包含 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 或 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 脚本。 对于 .aspx 文件编辑器，需要使用一种双语言体系结构，以便为 HTML 和脚本语言提供 IntelliSense、着色和其他编辑功能。  
  
## <a name="implementation"></a>实现  
 为包含的语言实现所需的最重要的接口是 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> 接口。 此接口由可在主要语言中托管的任何语言实现。 它允许访问语言服务的 colorizer、文本视图筛选器和主要语言服务 ID。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory>使您能够创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> 接口。 以下步骤演示如何实现包含的语言：  
  
1. 使用 `QueryService()` 可获取的语言服务 id 和的接口 id <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory.GetLanguage%2A> 方法以创建 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> 接口。 传递 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 接口、一个或多个 [项 id](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>) 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator> 接口。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>接口是文本缓冲区协调器对象，提供将主文件中的位置映射到辅助语言的缓冲区所需的基本服务。  
  
     例如，在一个 .aspx 文件中，主文件包含 ASP、HTML 和包含的所有代码。 不过，辅助缓冲区只包含包含的代码和任何类定义，以使辅助缓冲区成为有效的代码文件。 缓冲区协调器处理将编辑从一个缓冲区协调到另一个缓冲区的工作。  
  
4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A>方法（它是主要语言）向缓冲区协调器通知其缓冲区中的哪些文本映射到辅助缓冲区中的相应文本。  
  
     语言在结构数组中传递，该数组 <xref:Microsoft.VisualStudio.TextManager.Interop.NewSpanMapping> 当前只包含一个主范围和一个辅助跨度。  
  
5. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapPrimaryToSecondarySpan%2A>方法和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapSecondaryToPrimarySpan%2A> 方法提供从主缓冲区到辅助缓冲区的映射，反之亦然。
