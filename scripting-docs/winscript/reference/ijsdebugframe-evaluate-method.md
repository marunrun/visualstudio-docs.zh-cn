---
title: 'Ijsdebugframe:: Evaluate 方法 |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugFrame.Evaluate
apilocation:
- jscript9diag.dll
ms.assetid: 0ee61340-37b8-4fbb-a028-748b5315e279
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b328d6071ae9dc96b8e7f62bad6d4417aa1730f4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62558185"
---
# <a name="ijsdebugframeevaluate-method"></a>IJsDebugFrame::Evaluate 方法
计算表达式的上下文中的此堆栈帧。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Evaluate(  
   LPCOLESTR pExpressionText,  
   IJsDebugProperty **ppDebugProperty,  
   BSTR *pError  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pExpressionText`  
 [in]要计算的表达式。  
  
 `ppDebugProperty`  
 [out]表示属性浏览器的对象。  
  
 `pError`  
 [out]错误消息，如果发生错误。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 返回以下信息：则为 S_OK:评估成功，* ppDebugProperty 包含计算结果。 S_FALSE:计算引发错误 （或不支持的求值运算） \*pError 包含错误消息。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugFrame 接口](../../winscript/reference/ijsdebugframe-interface.md)