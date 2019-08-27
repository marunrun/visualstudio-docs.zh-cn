---
title: IDebugApplication::RemoveStackFrameSniffer | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.RemoveStackFrameSniffer
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::RemoveStackFrameSniffer
ms.assetid: 00304b88-e435-4b87-a331-44e7492eb32d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1462ff1382f3ccb844ccc98c6e6eec676a86c669
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990773"
---
# <a name="idebugapplicationremovestackframesniffer"></a>IDebugApplication::RemoveStackFrameSniffer
删除此应用程序中的堆栈帧的枚举器提供程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT RemoveStackFrameSniffer(  
   DWORD  dwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwCookie`  
 [in]返回的 cookie`AddStackFrameSniffer`方法时的堆栈帧的枚举器提供程序已添加。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 `RemoveStackFrameSniffer`方法从该应用程序中移除的堆栈帧的枚举器提供程序。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication::AddStackFrameSniffer](../../winscript/reference/idebugapplication-addstackframesniffer.md)   
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IDebugStackFrameSniffer 接口](../../winscript/reference/idebugstackframesniffer-interface.md)