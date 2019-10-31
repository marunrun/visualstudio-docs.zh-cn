---
title: VSCodeWindow 对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 36b7e0e6806f88efe373dffa3f21ba79baefb281
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189049"
---
# <a name="vscodewindow-object"></a>VSCodeWindow 对象
代码窗口是一个专用的文档窗口，它可以包含一个或多个文本视图，通常是 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> 对象。

 在体系结构上，代码窗口是窗口框架内的文档窗口。 在功能上，代码窗口只是包含附加功能的文档窗口。 在多文档界面（MDI）模式下，代码窗口是 MDI 子框架。 有关详细信息，请参阅[使用旧版 API 自定义代码窗口](/visualstudio/extensibility/customizing-code-windows-by-using-the-legacy-api?view=vs-2015)。

 下表包括 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> 对象中的接口。

|方法|描述|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|提供用于查找全局唯一标识符（GUID）标识的服务的通用访问机制。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|表示包含一个或多个代码视图的多文档界面（MDI）子对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|填充窗口框架。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [编辑图形](https://www.microsoft.com/download/details.aspx?id=55984)