---
title: ICanHandleException::CanHandleException | Microsoft Docs
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
ms.openlocfilehash: 406787d5ee6811b80f9e6831e5a67cab8367e7d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991386"
---
# <a name="icanhandleexceptioncanhandleexception"></a>ICanHandleException::CanHandleException
确定是否脚本引擎的调用方可以处理指定的异常。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CanHandleException(  
   EXCEPINFO*  pExcepInfo,  
   VARIANT*    pvar  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pExcepInfo`  
 [in]指向`EXCEPINFO`结构，它包含不发现任何异常处理程序的情况下报告的信息。  
  
 `pvar`  
 [in]关联的异常，如引发的值的值`throw`语句。 此参数可以为 `NULL`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|调用方可以处理异常|  
|`E_FAIL`|调用方无法处理该异常。|  
  
## <a name="remarks"></a>备注  
 如果调用`IDispatchEx::InvokeEx`，或类似的方法会导致异常，支持的脚本的调用方链中的调用方的脚本引擎检查`ICanHandleException`接口，并指示它能够处理该异常。 如果没有调用方可以处理异常，脚本引擎就会停止。  
  
## <a name="see-also"></a>请参阅  
 [ICanHandleException 接口](../../winscript/reference/icanhandleexception-interface.md)   
 [IDispatchEx::InvokeEx](../../winscript/reference/idispatchex-invokeex.md)