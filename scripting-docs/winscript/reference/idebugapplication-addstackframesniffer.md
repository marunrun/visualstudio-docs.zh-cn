---
title: IDebugApplication::AddStackFrameSniffer | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.AddStackFrameSniffer
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::AddStackFrameSniffer
ms.assetid: a7a9684a-14c5-415a-ae63-a17397d58d07
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 16fb941a91482c548284dc3d4317a472fd9be641
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991054"
---
# <a name="idebugapplicationaddstackframesniffer"></a>IDebugApplication::AddStackFrameSniffer
将堆栈帧的枚举器提供程序添加到此应用程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddStackFrameSniffer(  
   IDebugStackFrameSniffer*  pdsfs,  
   DWORD*                    pdwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdsfs`  
 [in]堆栈帧的枚举器提供程序添加到此应用程序。  
  
 `pdwCookie`  
 [out]一个用于从应用程序中删除此堆栈帧的枚举器提供程序的 cookie。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 尽管通常情况下，语言引擎调用此方法，以公开到调试器其堆栈帧，就可以为其他实体公开堆栈帧。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IDebugApplication::RemoveStackFrameSniffer](../../winscript/reference/idebugapplication-removestackframesniffer.md)   
 [IDebugStackFrameSniffer 接口](../../winscript/reference/idebugstackframesniffer-interface.md)