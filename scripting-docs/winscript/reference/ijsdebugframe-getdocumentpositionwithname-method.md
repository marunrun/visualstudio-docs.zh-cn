---
title: 'Ijsdebugframe:: Getdocumentpositionwithname 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.GetDocumentPositionWithName
apilocation:
- jscript9diag.dll
ms.assetid: 1d994714-2c87-4a9e-ae14-a15eec9520c7
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4d3b909f3a3ebc672bf6d0a014b519de685b1677
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62558146"
---
# <a name="ijsdebugframegetdocumentpositionwithname-method"></a>IJsDebugFrame::GetDocumentPositionWithName 方法
返回此堆栈帧的用户级别文档中的当前位置。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocumentPositionWithName(  
   BSTR *pDocumentName,  
   DWORD *pLine,  
   DWORD *pColumn  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pDocumentName`  
 [out]用于静态脚本，文档的 URL。 针对动态脚本，则返回包含脚本 （例如，eval 代码，函数代码等） 的类型的名称。  
  
 `pLine`  
 [out] 在文档中的基于 1 的行位置。  
  
 `pColumn`  
 [out] 在文档中的基于 1 的行位置。  
  
## <a name="return-value"></a>返回值  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugFrame 接口](../../winscript/reference/ijsdebugframe-interface.md)