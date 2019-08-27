---
title: 包含语言 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184276"
---
# <a name="contained-languages"></a>包含的语言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)] 

*包含语言*是所包含的其他语言的语言。 例如，在 HTML[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]可能包含页[!INCLUDE[csprcs](../includes/csprcs-md.md)]或[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]脚本。 .Aspx 文件编辑器为 HTML 和脚本语言提供 IntelliSense、 着色、 和其他编辑功能需要双语言体系结构。  
  
## <a name="implementation"></a>实现  
 您需要实现包含语言的最重要的接口是<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage>接口。 此接口实现的任何语言都可以承载于主要语言内。 它允许访问语言服务的着色器、 文本视图筛选器和主要语言服务 id。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory>使您能够创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage>接口。 以下步骤演示如何实现包含的语言：  
  
1. 使用`QueryService()`以获取语言服务 ID 和的接口 ID <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory>。  
  
2. 调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory.GetLanguage%2A>方法来创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage>接口。 传递<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口，一个或多个[项 Id](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>)和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>接口。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>接口，这是文本缓冲区处理协调器对象，提供了将映射到辅助语言的缓冲区中主文件的位置所需的基本服务。  
  
     例如，在一个.aspx 文件中，主文件将包括 ASP、 HTML 和包含的所有代码。 但是，次要缓冲区，包括仅包含的代码，以及任何类定义，以使辅助缓冲区有效的代码文件。 缓冲区处理协调器处理的协调对另一个缓冲区中的编辑的工作。  
  
4. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A>方法，它是主要语言，指示缓冲区处理协调器什么文本内其缓冲区映射到辅助缓冲区中的相应文本。  
  
     该语言将在一个数组中传递<xref:Microsoft.VisualStudio.TextManager.Interop.NewSpanMapping>结构当前只包括一个主证书和辅助跨度。  
  
5. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapPrimaryToSecondarySpan%2A>方法和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapSecondaryToPrimarySpan%2A>方法提供的映射从主数据库到辅助缓冲区，反之亦然。
