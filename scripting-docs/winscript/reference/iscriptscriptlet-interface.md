---
title: IScriptScriptlet Interface | Microsoft Docs
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
ms.openlocfilehash: c11aada6b8c39c7dd5f0b2a6b30cdd837aa0edda
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786706"
---
# <a name="iscriptscriptlet-interface"></a>IScriptScriptlet 接口
一个对象，实现`IScriptScriptlet`接口表示一个事件处理程序脚本。  
  
 除了继承的方法之外`IScriptEntry`，则`IScriptScriptlet`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IScriptScriptlet::GetEventName](../../winscript/reference/iscriptscriptlet-geteventname.md)|返回与 scriptlet 相关联的事件的名称。|  
|[IScriptScriptlet::GetSimpleEventName](../../winscript/reference/iscriptscriptlet-getsimpleeventname.md)|返回与 scriptlet 相关联的简单事件名称。 这是不包含任何空白区域的单个词名称。|  
|[IScriptScriptlet::GetSubItemName](../../winscript/reference/iscriptscriptlet-getsubitemname.md)|Scriptlet 的对象主机的完全限定名称中返回的最后一个标识符。|  
|[IScriptScriptlet::SetEventName](../../winscript/reference/iscriptscriptlet-seteventname.md)|设置与 scriptlet 相关联的事件的名称。|  
|[IScriptScriptlet::SetSimpleEventName](../../winscript/reference/iscriptscriptlet-setsimpleeventname.md)|设置与 scriptlet 相关联的简单事件名称。 这是不包含任何空白区域的单个词名称。|  
|[IScriptScriptlet::SetSubItemName](../../winscript/reference/iscriptscriptlet-setsubitemname.md)|Scriptlet 的对象主机的完全限定名称中设置的最后一个标识符。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本创作接口](../../winscript/reference/active-script-authoring-interfaces.md)