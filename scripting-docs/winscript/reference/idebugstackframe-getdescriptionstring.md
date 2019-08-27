---
title: IDebugStackFrame::GetDescriptionString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugStackFrame.GetDescriptionString
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugStackFrame::GetDescriptionString
ms.assetid: a2ddc069-c440-4dee-98dc-ab7c78773b94
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f870c6dbc654f8465d201c53443228153ce4a68b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934615"
---
# <a name="idebugstackframegetdescriptionstring"></a>IDebugStackFrame::GetDescriptionString
返回的堆栈帧的短期或长文本描述。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDescriptionString(  
   BOOL   fLong,  
   BSTR*  pbstrDescription  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fLong`  
 [in]标志，其中`TRUE`返回的详细说明和`FALSE`返回的简短说明。  
  
 `pbstrDescription`  
 [out]堆栈帧的说明。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 通常情况下，如果`fLong`是`FALSE`，此方法提供仅与堆栈帧关联的函数的名称。 当`fLong`是`TRUE`，此方法还可以提供函数参数和其他相关信息。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrame 接口](../../winscript/reference/idebugstackframe-interface.md)