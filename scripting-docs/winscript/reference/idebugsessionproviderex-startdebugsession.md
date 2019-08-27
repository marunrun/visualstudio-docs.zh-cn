---
title: IDebugSessionProviderEx:StartDebugSession | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugSessionProviderEx:StartDebugSession
apilocation:
- scrobj.dll
ms.assetid: 247337ca-476c-4aa7-8500-d84fd1d98176
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fb120a9acca91014d7b8213a3ed0bd1ab575e118
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934688"
---
# <a name="idebugsessionproviderexstartdebugsession"></a>IDebugSessionProviderEx:StartDebugSession
启动具有指定的应用程序的调试会话。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT StartDebugSession(  
   IRemoteDebugApplication*  pda  
   BOOL  fQuery  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pda`  
 [in]指定调试应用程序。  
  
 `fQuery`  
 [in]True 表示查询。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法会启动与指定的应用程序的调试会话。 调试程序应调用`IRemoteDebugApplication::ConnectDebugger`之前从该调用返回。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSessionProviderEx 接口](../../winscript/reference/idebugsessionproviderex-interface.md)   
 [IRemoteDebugApplication::ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)