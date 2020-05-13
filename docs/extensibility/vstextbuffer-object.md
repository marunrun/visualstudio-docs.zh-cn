---
title: VSText缓冲区对象 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5ea44d2b22c96d49f334f2ea33f9db8d69b5eb0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697728"
---
# <a name="vstextbuffer-object"></a>VSTextBuffer 对象
文本缓冲区对象表示 Unicode 文本流，通常与文件关联。 对象<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>可以在核心编辑器的上下文之外使用，如向导。

 下表显示了 的`VSTextBuffer`接口。

|方法|描述|
|------------|-----------------|
|[IOleCommand目标](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|标准 OLE 接口。 用于在缓冲区中撤消/重做处理。|
|[IPersist文件](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|标准 OLE 接口。|
|[I坚持流](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|标准 OLE 接口。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|启用创建复合操作（即，在单个撤消/重做单元中分组的操作）。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|启用由文本缓冲区管理的文档数据的持久性。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|提供基本服务;许多客户端使用。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|用于搜索缓冲区。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|使用二维坐标提供读写功能。 继承自 `IVsTextBuffer`。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|使用一维坐标提供读写功能。 继承自 `IVsTextBuffer`。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|提供对缓冲区中文本的快速、面向流的顺序访问。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|提供对属性的通用集合的访问。 最重要的属性是缓冲区的名称或名称。 通过创建 GUID 并将其用作密钥，可以使用此接口将您自己的随机数据存储在缓冲区中。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|支持事件的连接点。|

## <a name="remarks"></a>备注
 `VSTextBuffer`通常通过`QueryInterface`调用`IVsTextBuffer`找到 。 有关详细信息，请参阅[文本缓冲区](/visualstudio/extensibility/accessing-the-text-buffer-by-using-the-legacy-api?view=vs-2015)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>
- <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>
- [数字编辑](https://www.microsoft.com/download/details.aspx?id=55984)
