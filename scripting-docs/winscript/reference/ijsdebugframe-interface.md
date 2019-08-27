---
title: IJsDebugFrame 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 5af46b18-9d25-4a23-b8d1-fa23bea3efcf
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 57f5a848967148705a2b8dcd3f6b75dcb3a5db26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557998"
---
# <a name="ijsdebugframe-interface"></a>IJsDebugFrame 接口
表示堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp
IJsDebugFrame : public IUnknown;  
```  
  
## <a name="members"></a>成员  
  
### <a name="public-methods"></a>公共方法  
  
|名称|描述|  
|----------|-----------------|  
|[IJsDebugFrame::Evaluate 方法](../../winscript/reference/ijsdebugframe-evaluate-method.md)|计算表达式的上下文中的此堆栈帧。|  
|[IJsDebugFrame::GetDebugProperty 方法](../../winscript/reference/ijsdebugframe-getdebugproperty-method.md)|返回此堆栈帧的属性浏览器。|  
|[IJsDebugFrame::GetDocumentPositionWithId 方法](../../winscript/reference/ijsdebugframe-getdocumentpositionwithid-method.md)|返回此堆栈帧的用户级别文档中的当前位置。|  
|[IJsDebugFrame::GetDocumentPositionWithName 方法](../../winscript/reference/ijsdebugframe-getdocumentpositionwithname-method.md)|返回此堆栈帧的用户级别文档中的当前位置。|  
|[IJsDebugFrame::GetName 方法](../../winscript/reference/ijsdebugframe-getname-method.md)|获取堆栈帧的用户友好名称。|  
|[IJsDebugFrame::GetReturnAddress 方法](../../winscript/reference/ijsdebugframe-getreturnaddress-method.md)|获取 start 返回地址 （请参阅 GetStackRange） 的框架。|  
|[IJsDebugFrame::GetStackRange 方法](../../winscript/reference/ijsdebugframe-getstackrange-method.md)|返回逻辑 JavaScript 堆栈帧的绝对地址范围。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)