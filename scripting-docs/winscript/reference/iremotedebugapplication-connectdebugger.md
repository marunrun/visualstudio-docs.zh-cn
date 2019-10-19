---
title: IRemoteDebugApplication：： ConnectDebugger |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplication.ConnectDebugger
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplication::ConnectDebugger
ms.assetid: ded94101-7efe-466f-aa70-b3e30a38c4d8
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ed0ddeffd55475e1be4c9fab1e567d61a4b6654
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572319"
---
# <a name="iremotedebugapplicationconnectdebugger"></a>IRemoteDebugApplication::ConnectDebugger
将调试器连接到此应用程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ConnectDebugger(  
   IApplicationDebugger*  pad  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pad`  
 中要附加到此应用程序的调试器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|调试器已经连接到此应用程序。|  
  
## <a name="remarks"></a>备注  
 一个应用程序一次只能连接一个调试器。 如果调试器已连接，则此方法将失败。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication：： GetDebugger](../../winscript/reference/iremotedebugapplication-getdebugger.md)    
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)