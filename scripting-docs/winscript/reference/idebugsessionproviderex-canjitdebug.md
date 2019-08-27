---
title: IDebugSessionProviderEx:CanJITDebug | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugSessionProviderEx:CanJITDebug
apilocation:
- scrobj.dll
ms.assetid: 68f91bed-ca69-46b5-b517-ca9ca80b8803
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 295be698e02264c81522b70d0377c2030da6190e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979004"
---
# <a name="idebugsessionproviderexcanjitdebug"></a>IDebugSessionProviderEx:CanJITDebug
确定指定的进程是否可调试实时调试。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CanJITDebug(  
   DWORD  pid  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pid`  
 [in]要调试的进程的进程标识符。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IDebugSessionProviderEx 接口](../../winscript/reference/idebugsessionproviderex-interface.md)