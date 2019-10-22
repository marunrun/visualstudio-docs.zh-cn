---
title: IScriptEntry 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IScriptEntry interface
ms.assetid: 86da3bc1-58b7-4d73-87ab-bc3ce34e3f41
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 868322358908a32c8f14b56846cf3237f8531b4c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575399"
---
# <a name="iscriptentry-interface"></a>IScriptEntry 接口
实现 `IScriptEntry` 接口的对象表示脚本块或函数对象。  
  
 除了从 `IScriptNode` 继承的方法之外，`IScriptEntry` 接口还公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IScriptEntry::GetBody](../../winscript/reference/iscriptentry-getbody.md)|返回与 `IScriptEntry` script 块、function 块或 scriptlet 的主体对应的文本。|  
|[IScriptEntry::GetItemName](../../winscript/reference/iscriptentry-getitemname.md)|返回标识 `IScriptEntry` 对象的项名称。|  
|[IScriptEntry::GetName](../../winscript/reference/iscriptentry-getname.md)|对于表示单个对象的项（如函数），返回对象的名称。|  
|[IScriptEntry::GetRange](../../winscript/reference/iscriptentry-getrange.md)|返回项的开始位置和长度。|  
|[IScriptEntry::GetSignature](../../winscript/reference/iscriptentry-getsignature.md)|返回 `IScriptEntry` 函数对象的类型信息。|  
|[IScriptEntry::GetText](../../winscript/reference/iscriptentry-gettext.md)|返回与 `IScriptEntry` 脚本块对应的文本，或包含在 `IScriptScriptlet` 事件处理程序中的源代码。|  
|[IScriptEntry::SetBody](../../winscript/reference/iscriptentry-setbody.md)|设置位于 `IScriptEntry` 脚本块或 `IScriptScriptlet` scriptlet 正文中的文本。|  
|[IScriptEntry::SetItemName](../../winscript/reference/iscriptentry-setitemname.md)|设置标识 `IScriptEntry` 对象的项名称。|  
|[IScriptEntry::SetName](../../winscript/reference/iscriptentry-setname.md)|对于表示单个对象的项（如函数），设置该对象的名称。|  
|[IScriptEntry::SetSignature](../../winscript/reference/iscriptentry-setsignature.md)|设置 `IScriptEntry` 函数对象的类型信息。|  
|[IScriptEntry::SetText](../../winscript/reference/iscriptentry-settext.md)|设置与 `IScriptEntry` 脚本块对应的文本，或包含在 `IScriptScriptlet` 事件处理程序中的源代码。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本创作接口](../../winscript/reference/active-script-authoring-interfaces.md)