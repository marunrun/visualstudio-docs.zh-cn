---
title: VSCodeWindow Object | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 511c730ec3a11b02d46f5e9c9271c028bb4fa325
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690777"
---
# <a name="vscodewindow-object"></a>VSCodeWindow 对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

代码窗口是可以包含一个或多个文本视图，通常一个专用的文档窗口<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>对象。  
  
 体系结构方面，代码窗口是窗口框架中是一个文档窗口。 就功能而言，代码窗口是只需具有其他功能的文档窗口。 在多文档界面 (MDI) 模式下，代码窗口是 MDI 子框架。 有关详细信息，请参阅[使用旧版 API 自定义代码 Windows](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)。  
  
 下表包含中的接口<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>对象。  
  
|方法|描述|  
|------------|-----------------|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|提供的通用访问机制来查找全局唯一标识符 (GUID) 标识的服务。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|表示多文档界面 (MDI) 子包含一个或多个代码视图。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|填充窗口框架。|  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>   
 [图编辑](https://msdn.microsoft.com/f08872bd-fd9c-4e36-8cf2-a2a2622ef986)
