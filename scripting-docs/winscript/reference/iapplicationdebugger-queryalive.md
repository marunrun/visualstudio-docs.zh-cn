---
title: IApplicationDebugger::QueryAlive |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.QueryAlive
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::QueryAlive
ms.assetid: 41181ebb-a3bf-4e41-82af-d6c7348dc706
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b4c455305116863a4a8ad16ff21cd7554a36239
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991183"
---
# <a name="iapplicationdebuggerqueryalive"></a>IApplicationDebugger::QueryAlive
指示调试器是否响应。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT QueryAlive();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法指示调试器是否响应。 此方法的实现应始终返回`S_OK`。  
  
 如果调试器进程意外终止，COM 从封送处理代理对此方法的调用将返回错误。  
  
## <a name="see-also"></a>请参阅  
 [IApplicationDebugger 接口](../../winscript/reference/iapplicationdebugger-interface.md)