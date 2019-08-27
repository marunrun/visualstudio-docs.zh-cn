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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204643"
---
# <a name="drop-down-bar"></a>下拉栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

下拉栏顶部的代码窗口提供，包含两个下拉列表。  
  
## <a name="drop-down-bar-interfaces"></a>下拉栏接口  
 在中[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]，例如，下拉栏包含列表[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]项和[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]项成员函数，如下图中所示。  
  
 ![删除&#45;向下条](../extensibility/media/vsdropdown-bar.gif "vsDropdown_bar")  
下拉栏  
  
 在实现时的下拉条，有四个最为重要的接口：  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient>  
  
     实现此接口可插入下拉栏的内容。 每个下拉列表组合可以包含纯文本或复杂的文本 (粗体、 下划线或斜体)，可以有窗口的文本字体颜色设置或灰色的字体颜色设置，并可以选择性地提供下拉列表项旁边的小位图。 类似于<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>接口，位图图像提供图像列表中。 每个下拉列表组合可以具有不同的图像列表;但是，每个图像列表必须包含图像的高度相同。 此外，使用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarClient.GetComboTipText%2A>方法，您可以为每个组合提供工具提示。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager>  
  
     调用此接口可创建或销毁代码窗口的下拉栏。 此接口还可用于确定是否下拉栏已附加到代码窗口通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A>方法。 调用<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>有关<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager>从<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar>  
  
     调用此接口可直接与下拉栏进行通信。 可以使用此接口来强制刷新下拉列表内容栏或若要更改一个列表框中的选择。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents>  
  
     如果你注册`ShowDropdownBarOption`中你的语言服务注册表项，然后在代码窗口管理器必须监视此事件与用户首选项有关是否应显示在下拉栏进行同步。 如果你的语言服务密钥，在不注册此选项，则上禁用了选项后，可以显示或隐藏下拉栏**选项**菜单。  
  
## <a name="attaching-a-drop-down-bar-to-a-code-window"></a>附加到代码窗口的下拉条  
 若要附加的下拉条到代码窗口中，在创建时，语言服务应附加到下拉控件栏时<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A>调用方法。 如果调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.GetDropdownBar%2A>方法指示下拉栏不尚不存在，则调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager.AddDropdownBar%2A>。 访问<xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBarManager>接口中，调用<xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A>从<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>指针返回给您时你<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>实现已附加。  
  
## <a name="see-also"></a>请参阅  
 [通过使用旧版 API 自定义代码 Windows](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)   
 [旧版语言服务中的导航栏支持](../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)
