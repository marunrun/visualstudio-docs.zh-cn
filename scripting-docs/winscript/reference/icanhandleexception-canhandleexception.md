---
title: ICanHandleException：： CanHandleException |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ICanHandleException.CanHandleException
apilocation:
- scrobj.dll
helpviewer_keywords:
- ICanHandleException::CanHandleException
ms.assetid: 0fc703bf-9518-487e-af20-00e073b640f1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c536d35dcb9f0faca8b033ecd39aec520a2e260a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575719"
---
# <a name="icanhandleexceptioncanhandleexception"></a>ICanHandleException::CanHandleException
确定脚本引擎的调用方是否可以处理指定的异常。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CanHandleException(  
   EXCEPINFO*  pExcepInfo,  
   VARIANT*    pvar  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pExcepInfo`  
 中指向 `EXCEPINFO` 结构的指针，该结构包含在未找到异常处理程序时将报告的信息。  
  
 `pvar`  
 中与异常关联的值，如 `throw` 语句引发的值。 此参数可以为 `NULL`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|调用方可以处理异常|  
|`E_FAIL`|调用方无法处理此异常。|  
  
## <a name="remarks"></a>备注  
 如果调用 `IDispatchEx::InvokeEx` 或类似方法导致异常，则脚本引擎将在支持 `ICanHandleException` 接口的脚本调用方链中检查调用方，并指示它可以处理该异常。 如果调用方不能处理异常，则脚本引擎将暂停。  
  
## <a name="see-also"></a>请参阅  
 [ICanHandleException 接口](../../winscript/reference/icanhandleexception-interface.md)   
 [IDispatchEx::InvokeEx](../../winscript/reference/idispatchex-invokeex.md)