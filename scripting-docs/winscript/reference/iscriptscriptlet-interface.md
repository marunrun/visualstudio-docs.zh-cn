---
title: IScriptScriptlet 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IScriptScriptlet interface
ms.assetid: b9981908-a337-4228-864c-c741f111ab2d
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7b7973aee209695592f022d0e05a770caa1e694c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571883"
---
# <a name="iscriptscriptlet-interface"></a>IScriptScriptlet 接口
实现 `IScriptScriptlet` 接口的对象表示事件处理程序脚本。  
  
 除了从 `IScriptEntry` 继承的方法之外，`IScriptScriptlet` 接口还公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IScriptScriptlet::GetEventName](../../winscript/reference/iscriptscriptlet-geteventname.md)|返回与 scriptlet 关联的事件的名称。|  
|[IScriptScriptlet:: GetSimpleEventName](../../winscript/reference/iscriptscriptlet-getsimpleeventname.md)|返回与 scriptlet 关联的简单事件名称。 这是一个不包含任何空格的单字名称。|  
|[IScriptScriptlet::GetSubItemName](../../winscript/reference/iscriptscriptlet-getsubitemname.md)|返回 scriptlet 的对象主机的完全限定名中的最后一个标识符。|  
|[IScriptScriptlet::SetEventName](../../winscript/reference/iscriptscriptlet-seteventname.md)|设置与 scriptlet 关联的事件的名称。|  
|[IScriptScriptlet::SetSimpleEventName](../../winscript/reference/iscriptscriptlet-setsimpleeventname.md)|设置与 scriptlet 关联的简单事件名称。 这是一个不包含任何空格的单字名称。|  
|[IScriptScriptlet::SetSubItemName](../../winscript/reference/iscriptscriptlet-setsubitemname.md)|设置 scriptlet 的对象主机的完全限定名中的最后一个标识符。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本创作接口](../../winscript/reference/active-script-authoring-interfaces.md)