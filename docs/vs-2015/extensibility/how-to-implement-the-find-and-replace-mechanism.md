---
title: 如何：实现查找和替换机制 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - find and replace
ms.assetid: bbd348db-3d19-42eb-99a2-3e808528c0ca
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d4362d0b0c3f013ce6f38d13265dcc181c77012c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62548687"
---
# <a name="how-to-implement-the-find-and-replace-mechanism"></a>如何：实现查找和替换机制
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 提供了两种实现查找/替换的方式。 一种方法是将文本图像传递到 shell，并使其处理搜索、突出显示和替换文本。 这允许用户指定多个文本范围。 或者，你的 VSPackage 可以控制此功能本身。 在这两种情况下，您必须通知 shell 有关当前目标和所有打开文档的目标的信息。  
  
### <a name="to-implement-findreplace"></a>实现查找/替换  
  
1. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>在由框架属性或返回的对象之一上实现接口 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> 。 如果要创建自定义编辑器，则应将此接口作为自定义编辑器类的一部分实现。  
  
2. 使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.GetCapabilities%2A> 方法指定编辑器支持的选项，并指示它是否实现文本图像搜索。  
  
     如果编辑器支持文本图像搜索，请实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.GetSearchImage%2A> 。  
  
     否则，实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A> 。  
  
3. 如果实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A> 方法，则可以通过调用接口简化搜索任务 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindHelper> 。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindHelper>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.GetSearchImage%2A>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
