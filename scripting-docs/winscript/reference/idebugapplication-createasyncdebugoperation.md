---
title: IDebugApplication::CreateAsyncDebugOperation | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.CreateAsyncDebugOperation
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::CreateAsyncDebugOperation
ms.assetid: bc32b101-6364-4498-8458-bd5f3ab5ad94
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c60c84dbd3be9248e2bd075e65d53f7f9361d0b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991014"
---
# <a name="idebugapplicationcreateasyncdebugoperation"></a>IDebugApplication::CreateAsyncDebugOperation
提供对给定同步调试操作的异步访问。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateAsyncDebugOperation(  
   IDebugSyncOperation*    psdo,  
   IDebugAsyncOperation**  ppado  
);  
```  
  
#### <a name="parameters"></a>参数  
 `psdo`  
 [in]同步调试操作对象。  
  
 `ppado`  
 [out]异步调试操作对象。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法允许语言引擎来以异步方式计算表达式，而无需显式同步与调试器线程。 有关详细信息，请参阅[IDebugSyncOperation 接口](../../winscript/reference/idebugsyncoperation-interface.md)并[IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplication 接口](../../winscript/reference/idebugapplication-interface.md)   
 [IDebugSyncOperation 接口](../../winscript/reference/idebugsyncoperation-interface.md)   
 [IDebugAsyncOperation 接口](../../winscript/reference/idebugasyncoperation-interface.md)