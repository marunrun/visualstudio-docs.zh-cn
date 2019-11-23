---
title: ISimpleConnectionPoint：： Advise |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISimpleConnectionPoint.Advise
apilocation:
- pdm.dll
helpviewer_keywords:
- ISimpleConnectionPoint::Advise
ms.assetid: 59ded60d-b938-4110-aca3-e69ba234ca9a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d7d08d4774dffbfd840c674b15abe82bedb37e5f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571835"
---
# <a name="isimpleconnectionpointadvise"></a>ISimpleConnectionPoint::Advise
在简单连接点对象和客户端接收器之间建立连接。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Advise(  
   IDispatch*  pdisp,  
   DWORD*      pdwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdisp`  
 中指向客户端的建议接收器上的 `IDispatch` 接口的指针。 客户端的接收器接收来自简单连接点的传出调用。  
  
 `pdwCookie`  
 弄指向唯一标识此连接的返回标记的指针。 调用方稍后使用此标记来删除连接，方法是将其传递到 `ISimpleConnectionPoint::Unadvise` 方法。 如果连接未成功建立，此值为零。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法在简单连接点对象和客户端接收器之间建立连接。  
  
## <a name="see-also"></a>另请参阅  
 [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)   
 [ISimpleConnectionPoint::Unadvise](../../winscript/reference/isimpleconnectionpoint-unadvise.md)