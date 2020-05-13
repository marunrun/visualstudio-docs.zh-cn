---
title: VSTextView 对象 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextView
helpviewer_keywords:
- VSTextView object, reference
- views [Visual Studio SDK], reference
ms.assetid: 78272ddc-9718-4c65-a94e-a44a2e8d54f4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81d5e02d6ec18f8561a83b414532a4b78def5c09
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697714"
---
# <a name="vstextview-object"></a>VSTextView 对象

文本视图是一个窗口，允许用户查看和编辑文本缓冲区的 Unicode 文本。 从本质上讲，视图是大多数用户所说的编辑器。 由于视图由各种文本图层（换行、大纲文本等）与缓冲区分开，因此不能保证视图是缓冲区中文本的精确表示形式。 有关文本视图的详细信息，请参阅[使用旧 API 访问文本视图](/visualstudio/extensibility/accessing-thetext-view-by-using-the-legacy-api?view=vs-2015)。

下表显示了对象中的<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>接口。

|接口|描述|
|---------------|-----------------|
|[IDrop来源](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|启用复合操作（即分组在单个撤消/重做单元中的操作）。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|提供管理和访问视图的基本方法。 `IVsTextView`不螺纹安全。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|创建和管理窗口窗格。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|与文本图层交互。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|从其他线程对视图执行操作。|

## <a name="see-also"></a>请参阅

- [数字编辑](https://www.microsoft.com/download/details.aspx?id=55984)
- [VSTextBuffer 对象](../extensibility/vstextbuffer-object.md)
