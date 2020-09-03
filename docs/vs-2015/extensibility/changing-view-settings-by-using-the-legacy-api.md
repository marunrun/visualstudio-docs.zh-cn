---
title: 使用旧版 API 更改视图设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - changing view settings
ms.assetid: 12c9b300-0894-4124-96a1-764326176d77
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7d58d1477b9d7f58242f8cb4db7c3c360c248b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184465"
---
# <a name="changing-view-settings-by-using-the-legacy-api"></a>使用旧版 API 更改视图设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

用户可以通过 " **选项** " 对话框更改核心编辑器功能（如自动换行、选择边距和虚拟空间）的设置。 不过，也可以通过编程方式更改这些设置。  
  
## <a name="changing-settings-by-using-the-legacy-api"></a>使用旧版 API 更改设置  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer>接口公开一组文本编辑器属性。 文本视图包含一类属性 (GUID_EditPropCategory_View_MasterSettings) ，表示文本视图的以编程方式更改的设置组。 一旦以这种方式更改视图设置，就不能在 " **选项** " 对话框中更改这些设置，除非重置。  
  
 下面是更改核心编辑器实例的视图设置的典型过程。  
  
1. 调用 `QueryInterface` 接口的 (<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>) <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> 。  
  
2. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A> 方法，将参数的值指定为 GUID_EditPropCategory_View_MasterSettings `rguidCategory` 。  
  
     执行此操作将返回一个指向接口的指针，该指针 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> 包含视图的强制属性集。 此组中的任何设置都将被永久强制执行。 如果某个设置不在此组中，则它将遵循在 " **选项** " 对话框或用户的命令中指定的选项。  
  
3. 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> 方法，并在参数中指定适当的设置值 `idprop` 。  
  
     例如，若要强制自动换行，请调用， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> 并为参数指定 VSEDITPROPID_ViewLangOpt_WordWrap 的值 `vt` `idprop` 。 在此调用中， `vt` 是 VT_BOOL 类型的变体，并且 `vt.boolVal` VARIANT_TRUE。  
  
## <a name="resetting-changed-view-settings"></a>正在重置更改的视图设置  
 若要重置核心编辑器实例的任何已更改的视图设置，请调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.RemoveProperty%2A> 方法，并在参数中指定适当的设置值 `idprop` 。  
  
 例如，若要允许自动换行，可以通过调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.RemoveProperty%2A> 并为参数指定 VSEDITPROPID_ViewLangOpt_WordWrap 值，将其从属性类别中移除 `idprop` 。  
  
 若要同时删除核心编辑器的所有已更改设置，请将参数的值指定为 VSEDITPROPID_ViewComposite_AllCodeWindowDefaults `idprop` 。 在此调用中，vt 是 VT_BOOL 类型的变体，而 VARIANT_TRUE boolVal。  
  
## <a name="see-also"></a>另请参阅  
 [在核心编辑器内](../extensibility/inside-the-core-editor.md)   
 [使用旧 API 访问 theText 视图](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)   
 ["选项" 对话框](../ide/reference/options-dialog-box-visual-studio.md)
