---
title: IDebugStackFrame：： GetDebugProperty |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugStackFrame.GetDebugProperty
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugStackFrame::GetDebugProperty
ms.assetid: e03c7504-bce4-4a44-81e4-db8c0216538d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 452c08bb0319167c0dfc1de86bf38a993e3cbad8
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574270"
---
# <a name="idebugstackframegetdebugproperty"></a>IDebugStackFrame::GetDebugProperty
返回当前框架的属性浏览器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDebugProperty(  
   IDebugProperty**  ppDebugProp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppDebugProp`  
 弄当前框架的属性浏览器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法返回当前框架的属性浏览器。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrame 接口](../../winscript/reference/idebugstackframe-interface.md)