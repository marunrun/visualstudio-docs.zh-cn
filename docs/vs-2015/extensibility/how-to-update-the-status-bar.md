---
title: 如何：更新状态栏 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - update status bar
ms.assetid: 7500c8a7-4913-4818-a88b-bfd1b9887cb6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1d48b07dd5e4fc1fe745e3669041884c1b8eacd9
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703150"
---
# <a name="how-to-update-the-status-bar"></a>如何：更新状态栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**状态栏**控件条位于底部的多个应用程序窗口，其中包含一个或多个状态文本行或指示器。  
  
### <a name="to-update-the-status-bar"></a>若要更新状态栏  
  
1. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>提供你的编辑器，例如，窗体视图和代码视图的每个单独的视图对象 (DocView)。  
  
2. 当调用 IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>，更新中的信息**状态栏**通过调用的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>。  
  
    > [!NOTE]
    > IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>仅当文档窗口最初已激活。 文档窗口处于活动状态的时间的其余部分中，必须更新**状态栏**编辑器更改的状态信息。  
  
## <a name="robust-programming"></a>可靠编程  
 一个**状态栏**包含四个单独的字段：  
  
- 状态文本  
  
- 进度栏  
  
- 动画的图标  
  
- 编辑器的信息  
  
  有关详细信息，请参阅[状态栏](https://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)。  
  
  IDE 将自动调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>方法在<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>文档窗口被激活时实现。  
  
  VSPackage 实现器负责更新状态栏中的状态文本。 IDE 重置此字符串为"就绪"，如果 status 文本字段设置为空文本 ("") 在空闲时间。  
  
## <a name="see-also"></a>请参阅  
 [状态栏](https://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)
