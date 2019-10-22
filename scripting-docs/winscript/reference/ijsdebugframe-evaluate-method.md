---
title: IJsDebugFrame：：计算方法 |Microsoft Docs
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
ms.openlocfilehash: 6227b97c1fd5fae32db3e13ef72751726c36b043
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573500"
---
# <a name="ijsdebugframeevaluate-method"></a>IJsDebugFrame::Evaluate 方法
在此堆栈帧的上下文中计算表达式。  
  
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
 中要计算的表达式。  
  
 `ppDebugProperty`  
 弄表示属性浏览器的对象。  
  
 `pError`  
 弄错误消息（如果出现错误）。  
  
## <a name="return-value"></a>返回值  
  
## <a name="remarks"></a>备注  
 返回以下内容： S_OK：求值成功，* ppDebugProperty 包含计算结果。 S_FALSE：计算引发错误（或不支持求值运算），\*pError 包含错误消息。  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [IJsDebugFrame 接口](../../winscript/reference/ijsdebugframe-interface.md)