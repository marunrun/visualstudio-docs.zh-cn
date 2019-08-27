---
title: VSTextBuffer 对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5b68d443e542b6bd707aacc2b22d0efc1064152c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690645"
---
# <a name="vstextbuffer-object"></a>VSTextBuffer 对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本缓冲区对象表示 Unicode 文本，这是通常与文件相关联的流。 一个<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>下一个向导根据情况下，对象可以使用上下文之外的核心编辑器。  
  
 下表显示了接口的`VSTextBuffer`。  
  
|方法|描述|  
|------------|-----------------|  
|[IOleCommandTarget](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|标准 OLE 接口。 主要用于处理在缓冲区中撤消/重做。|  
|[IPersistFile](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|标准 OLE 接口。|  
|[IPersistStream](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|标准 OLE 接口。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|可以创建复合音操作 （即，在撤消/重做单个单元进行分组的操作）。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|使文档数据管理的文本缓冲区的持久性。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|提供基本服务;由多个客户端。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|用于搜索缓冲区。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|提供了读取和写入功能使用二维坐标。 继承自 `IVsTextBuffer`。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|提供了读取和写入功能使用一维的坐标。 继承自 `IVsTextBuffer`。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|提供快速、 面向流的顺序访问缓冲区中的文本。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|提供对属性的泛型集合的访问。 最重要属性是缓冲区的名称或的名字对象。 通过创建 GUID 并使用它作为键，可以使用此接口在缓冲区中存储自己的随机数据。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|支持连接点的事件。|  
  
## <a name="remarks"></a>备注  
 `VSTextBuffer`通常通过找到`QueryInterface`上调用`IVsTextBuffer`。 有关详细信息，请参阅[文本缓冲区](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 [图编辑](https://msdn.microsoft.com/f08872bd-fd9c-4e36-8cf2-a2a2622ef986)
