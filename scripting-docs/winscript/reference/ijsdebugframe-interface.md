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
ms.openlocfilehash: 91fe8cdf91b0c2121f4a1a7f111794b0fbe36669
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575106"
---
# <a name="ijsdebugframe-interface"></a>IJsDebugFrame 接口
表示堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp
IJsDebugFrame : public IUnknown;  
```  
  
## <a name="members"></a>Members  
  
### <a name="public-methods"></a>公共方法  
  
|“属性”|描述|  
|----------|-----------------|  
|[IJsDebugFrame::Evaluate 方法](../../winscript/reference/ijsdebugframe-evaluate-method.md)|在此堆栈帧的上下文中计算表达式。|  
|[IJsDebugFrame::GetDebugProperty 方法](../../winscript/reference/ijsdebugframe-getdebugproperty-method.md)|返回此堆栈帧的属性浏览器。|  
|[IJsDebugFrame::GetDocumentPositionWithId 方法](../../winscript/reference/ijsdebugframe-getdocumentpositionwithid-method.md)|返回此堆栈帧在用户级文档中的当前位置。|  
|[IJsDebugFrame::GetDocumentPositionWithName 方法](../../winscript/reference/ijsdebugframe-getdocumentpositionwithname-method.md)|返回此堆栈帧在用户级文档中的当前位置。|  
|[IJsDebugFrame::GetName 方法](../../winscript/reference/ijsdebugframe-getname-method.md)|获取堆栈帧的用户友好名称。|  
|[IJsDebugFrame::GetReturnAddress 方法](../../winscript/reference/ijsdebugframe-getreturnaddress-method.md)|获取以帧的 "start" （参见 GetStackRange）推送的返回地址。|  
|[IJsDebugFrame::GetStackRange 方法](../../winscript/reference/ijsdebugframe-getstackrange-method.md)|返回逻辑 JavaScript 堆栈帧的绝对地址范围。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)