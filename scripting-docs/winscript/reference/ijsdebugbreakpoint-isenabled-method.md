---
title: 'Ijsdebugbreakpoint:: Isenabled 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJSDebugBreakPoint.IsEnabled
apilocation:
- jscript9diag.dll
ms.assetid: 39b63f49-2a0d-41b7-a2ba-75dcb06251a9
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b99df17f73896b4dd04481315b04e1672a56285a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62583088"
---
# <a name="ijsdebugbreakpointisenabled-method"></a>IJsDebugBreakPoint::IsEnabled 方法
确定是否启用断点。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT IsEnabled(  
   BOOL *pIsEnabled  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pIsEnabled`  
 [out]如果已启用断点; 则返回 true否则，返回 false。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 如果对已删除的断点调用，则返回 E_UNEXPECTED。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugBreakPoint 接口](../../winscript/reference/ijsdebugbreakpoint-interface.md)