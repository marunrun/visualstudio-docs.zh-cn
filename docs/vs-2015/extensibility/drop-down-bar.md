---
title: 下拉栏 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - drop-down bar
ms.assetid: 4bb621bd-72f5-43d5-916f-9f66617da049
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7db4296a8fa4146a52d167bce3d8b051aa3ca073
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204643"
---
# <a name="drop-down-bar"></a>下拉栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下拉栏在代码窗口的顶部提供，并包含两个下拉列表。  
  
## <a name="drop-down-bar-interfaces"></a>下拉栏接口  
 例如，在中 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] ，下拉栏包含 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 项和 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] 项成员函数的列表，如下图所示。  
  
 ![拖放&#45;跌柱线](../extensibility/media/vsdropdown-bar.gif "vsDropdown_bar")  
下拉栏  
  
 实现下拉栏时，主要重要性有四个接口：  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient>  
  
     实现此接口可插入下拉栏的内容。 每个下拉组合都可以包含纯文本或纯文本 (粗体、下划线或斜体) ，可以使用窗口文本字体着色或灰显字体着色，还可以选择在下拉项旁边提供一个小位图。 类似于 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> 接口，图像列表中提供了位图图像。 每个下拉组合都可以具有不同的图像列表;但是，每个图像列表必须包含具有相同高度的图像。 此外，通过使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient.GetComboTipText%2A> 方法，您可以为每个组合提供工具提示。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager>  
  
     调用此接口可以创建或销毁代码窗口的下拉栏。 此接口还可用于确定是否已通过调用方法将下拉栏附加到代码窗口 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A> 。 <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>从调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>  
  
     调用此接口可直接与下拉栏通信。 您可以使用此接口来强制刷新下拉栏内容，或在其中一个列表框中更改所选内容。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents>  
  
     如果已 `ShowDropdownBarOption` 在语言服务注册表项中注册了，则代码窗口管理器必须监视此事件以与用户首选项同步，以了解是否应显示下拉栏。 如果未在语言服务密钥中注册此选项，则会在 " **选项** " 菜单上禁用用于显示或隐藏下拉栏的选项。  
  
## <a name="attaching-a-drop-down-bar-to-a-code-window"></a>将下拉栏附加到代码窗口  
 若要在创建时将下拉栏附加到代码窗口，语言服务应在调用方法时附加到下拉栏 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> 。 如果对方法的调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A> 指示下拉栏尚不存在，则调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.AddDropdownBar%2A> 。 若要访问 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager> 接口，请在 <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> 附加了实现时从返回的指针调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> 。  
  
## <a name="see-also"></a>另请参阅  
 [使用旧版 API 自定义代码窗口](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)   
 [旧版语言服务中的导航栏支持](../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)
