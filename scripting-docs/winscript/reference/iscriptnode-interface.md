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
ms.openlocfilehash: 13bf20f9e1e642b948ddaa72ae9dca7bb457fba2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786769"
---
# <a name="iscriptnode-interface"></a>IScriptNode 接口
一个对象，实现`IScriptNode`接口表示 Web 页。  
  
 除了继承的方法之外`IUnknown`，则`IScriptNode`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IScriptNode::Alive](../../winscript/reference/iscriptnode-alive.md)|指示对象是否仍处于活动状态。|  
|[IScriptNode::CreateChildEntry](../../winscript/reference/iscriptnode-createchildentry.md)|添加的子实例`IScriptEntry`。|  
|[IScriptNode::CreateChildHandler](../../winscript/reference/iscriptnode-createchildhandler.md)|将作为子实例添加 scriptlet `IScriptNode`。|  
|[IScriptNode::Delete](../../winscript/reference/iscriptnode-delete.md)|删除对象树。|  
|[IScriptNode::GetChild](../../winscript/reference/iscriptnode-getchild.md)|返回位于指定索引中的节点的子级。|  
|[IScriptNode::GetCookie](../../winscript/reference/iscriptnode-getcookie.md)|返回用于将 scriptlet 与该主机对象相关联的应用程序定义的值。|  
|[IScriptNode::GetIndexInParent](../../winscript/reference/iscriptnode-getindexinparent.md)|返回父级的子列表中的对象的索引。|  
|[IScriptNode::GetLanguage](../../winscript/reference/iscriptnode-getlanguage.md)|返回由当前的脚本节点的脚本语言。|  
|[IScriptNode::GetNumberOfChildren](../../winscript/reference/iscriptnode-getnumberofchildren.md)|返回的子节点数目`IScriptNode`对象。|  
|[IScriptNode::GetParent](../../winscript/reference/iscriptnode-getparent.md)|返回`IScriptNode`是父对象的对象。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本创作接口](../../winscript/reference/active-script-authoring-interfaces.md)