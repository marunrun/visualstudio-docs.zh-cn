---
title: 如何：在另一个编辑器中承载编辑器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - host a nested editor
ms.assetid: 2b0eb705-fe94-4ca8-93e0-9dbd8ce61a44
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4d4b4ff425feb22b5057a8d1a76b7f73b8932d9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204171"
---
# <a name="how-to-host-an-editor-in-another-editor"></a>如何：在编辑器中承载另一个编辑器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以通过将宿主窗口指定为父窗口，在另一个编辑器中托管一个编辑器。 为此，请 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> 在子窗口框架上设置参数和。  
  
### <a name="to-set-up-the-window-frame-to-host-an-editor"></a>设置窗口框架以承载编辑器  
  
1. 通过创建子窗口窗格，将编辑器指定为寄宿编辑器。  
  
     此窗格位于编辑器文本的位置。  
  
2. 使用或方法创建宿主编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A> 。  
  
3. 通过将 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID2> 这些属性分别作为参数传递给方法，在托管编辑器的窗口帧实现中设置和属性 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A> 。  
  
     如果需要检索这些参数，请将这些属性传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 方法。  
  
4. <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>为包含的编辑器调用方法。  
  
     编辑器显示在包含编辑器的 "承载" 窗格中。  
  
## <a name="robust-programming"></a>可靠编程  
 设计人员的 Visual Studio 团队版中的 **应用程序设计器** 是托管另一个编辑器的编辑器窗口框架的示例。 **应用程序设计器**在其右侧窗格中承载其他设计器。 将每个包含的设计器的 "设计器" 面板 (或 " **属性** " 页) 添加到包含窗口框架。
