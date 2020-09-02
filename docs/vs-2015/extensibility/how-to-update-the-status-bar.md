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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703150"
---
# <a name="how-to-update-the-status-bar"></a>如何：更新状态栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**状态栏**是位于多个应用程序窗口底部的控制条，其中包含一个或多个状态文本行或指示器。  
  
### <a name="to-update-the-status-bar"></a>更新状态栏  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>在编辑器提供的每个单独视图对象 (DocView) （如窗体视图和代码视图）上实现。  
  
2. 当 IDE 调用时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> ，通过调用的方法更新 **状态栏** 中的信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> 。  
  
    > [!NOTE]
    > IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 仅在最初激活文档窗口时调用。 对于文档窗口处于活动状态的剩余时间，必须更新 **状态栏** 信息，因为编辑器的状态发生更改。  
  
## <a name="robust-programming"></a>可靠编程  
 **状态栏**包含四个单独的字段：  
  
- 状态文本  
  
- 进度条  
  
- 动画图标  
  
- 编辑器信息  
  
  有关详细信息，请参阅 [状态栏](https://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)。  
  
  <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>激活文档窗口时，IDE 将自动调用实现的方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> 。  
  
  VSPackage 实施者负责更新状态栏中的状态文本。 如果状态文本字段设置为空文本，则 IDE 会将此字符串重置为 "READY"， ( "" ) 处于空闲时间。  
  
## <a name="see-also"></a>另请参阅  
 [状态栏](https://msdn.microsoft.com/library/fcbc5029-1aab-4e14-adf7-419038a4935e)
