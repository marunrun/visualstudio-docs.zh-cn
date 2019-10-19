---
title: IScriptNode 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IScriptNode interface
ms.assetid: cfa76c4a-6543-48e8-a946-d212cd0bf934
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 38ab73ddb1bd924035cb6ba61d26e65f16f53eed
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577506"
---
# <a name="iscriptnode-interface"></a>IScriptNode 接口
实现 `IScriptNode` 接口的对象表示网页。  
  
 除了从 `IUnknown` 继承的方法之外，`IScriptNode` 接口还公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IScriptNode::Alive](../../winscript/reference/iscriptnode-alive.md)|指示对象是否仍处于活动状态。|  
|[IScriptNode:: CreateChildEntry](../../winscript/reference/iscriptnode-createchildentry.md)|添加 `IScriptEntry` 的子实例。|  
|[IScriptNode::CreateChildHandler](../../winscript/reference/iscriptnode-createchildhandler.md)|添加 scriptlet 作为 `IScriptNode` 的子实例。|  
|[IScriptNode::Delete](../../winscript/reference/iscriptnode-delete.md)|删除对象树。|  
|[IScriptNode::GetChild](../../winscript/reference/iscriptnode-getchild.md)|返回位于节点中指定索引处的子级。|  
|[IScriptNode::GetCookie](../../winscript/reference/iscriptnode-getcookie.md)|返回应用程序定义的值，该值用于将 scriptlet 与宿主对象相关联。|  
|[IScriptNode::GetIndexInParent](../../winscript/reference/iscriptnode-getindexinparent.md)|返回父级的子列表中的对象的索引。|  
|[IScriptNode::GetLanguage](../../winscript/reference/iscriptnode-getlanguage.md)|返回当前脚本节点所使用的脚本语言。|  
|[IScriptNode::GetNumberOfChildren](../../winscript/reference/iscriptnode-getnumberofchildren.md)|返回 `IScriptNode` 对象的子节点数。|  
|[IScriptNode::GetParent](../../winscript/reference/iscriptnode-getparent.md)|返回作为对象的父对象的 `IScriptNode` 对象。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本创作接口](../../winscript/reference/active-script-authoring-interfaces.md)