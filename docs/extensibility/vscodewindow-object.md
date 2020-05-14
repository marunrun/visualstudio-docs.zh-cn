---
title: VSCode窗口对象 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 55739b1ef577123ac0395b4c5cfb1e3c5dbc779f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697957"
---
# <a name="vscodewindow-object"></a>VSCodeWindow 对象
代码窗口是一个专用文档窗口，可以包含一个或多个文本视图，通常是<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>对象。

 在体系结构上，代码窗口是窗口框架内的文档窗口。 在功能上，代码窗口只是具有附加功能的文档窗口。 在多文档接口 （MDI） 模式下，代码窗口是 MDI 子帧。 有关详细信息，请参阅[使用旧 API 自定义代码窗口](/visualstudio/extensibility/customizing-code-windows-by-using-the-legacy-api?view=vs-2015)。

 下表包括对象中的<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>接口。

|方法|描述|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|提供通用访问机制，用于查找全局唯一标识符 （GUID） 标识的服务。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|表示包含一个或多个代码视图的多个文档接口 （MDI） 子级。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|填充窗口框架。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [数字编辑](https://www.microsoft.com/download/details.aspx?id=55984)
