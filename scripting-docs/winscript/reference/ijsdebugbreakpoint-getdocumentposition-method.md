---
title: 'Ijsdebugbreakpoint:: Getdocumentposition 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJSDebugBreakPoint.GetDocumentPosition
apilocation:
- jscript9diag.dll
ms.assetid: 886df8ba-a59a-48a7-87f2-3b669e71528f
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 146eb26c887cd24d1eb7af858535fcecac62b41d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62583140"
---
# <a name="ijsdebugbreakpointgetdocumentposition-method"></a>IJsDebugBreakPoint::GetDocumentPosition 方法
返回绑定断点语句的位置。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocumentPosition(  
   UINT64 *pDocumentId,  
   DWORD *pCharacterOffset,  
   DWORD *pStatementCharCount  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pDocumentId`  
 [out]源文档 （指向 idebugdocumenttext 的指针） 的唯一 ID。  
  
 `pCharacterOffset`  
 [out]从脚本开始处的从零开始的字符偏移量。  
  
 `pStatementCharCount`  
 [out]当前语句开始处的长度 * pCharacterOffset，以字符为单位。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugBreakPoint 接口](../../winscript/reference/ijsdebugbreakpoint-interface.md)