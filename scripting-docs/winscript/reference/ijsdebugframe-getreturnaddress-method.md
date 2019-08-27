---
title: 'Ijsdebugframe:: Getreturnaddress 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.GetReturnAddress
apilocation:
- jscript9diag.dll
ms.assetid: 7f10c1d6-d7b9-402e-9020-04cded37f9d3
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 18b98c7a5f92f3745baea5d4f82ae90da0989135
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62558154"
---
# <a name="ijsdebugframegetreturnaddress-method"></a>IJsDebugFrame::GetReturnAddress 方法
获取 start 返回地址 （请参阅 GetStackRange） 的框架。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetReturnAddress(  
   UINT64 *pReturnAddress  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pReturnAddress`  
 [out]寄信人地址。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugFrame 接口](../../winscript/reference/ijsdebugframe-interface.md)