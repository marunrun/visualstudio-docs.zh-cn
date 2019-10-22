---
title: IJsDebugBreakPoint 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 791c8488-21e7-46be-b1b4-fe74117cf200
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6bb4e12f0e08baf1842d251347f35265425b999
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577680"
---
# <a name="ijsdebugbreakpoint-interface"></a>IJsDebugBreakPoint 接口
表示断点。  
  
## <a name="syntax"></a>语法  
  
```cpp
IJsDebugBreakPoint : public IUnknown;  
```  
  
## <a name="members"></a>Members  
  
### <a name="public-methods"></a>公共方法  
  
|“属性”|描述|  
|----------|-----------------|  
|[IJsDebugBreakPoint::Delete 方法](../../winscript/reference/ijsdebugbreakpoint-delete-method.md)|删除断点。|  
|[IJsDebugBreakPoint::Disable 方法](../../winscript/reference/ijsdebugbreakpoint-disable-method.md)|禁用断点。|  
|[IJsDebugBreakPoint::Enable 方法](../../winscript/reference/ijsdebugbreakpoint-enable-method.md)|启用断点。|  
|[IJsDebugBreakPoint::GetDocumentPosition 方法](../../winscript/reference/ijsdebugbreakpoint-getdocumentposition-method.md)|返回绑定断点的语句的位置。|  
|[IJsDebugBreakPoint::IsEnabled 方法](../../winscript/reference/ijsdebugbreakpoint-isenabled-method.md)|确定是否已启用断点。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)