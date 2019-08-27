---
title: ISimpleConnectionPoint::Advise |Microsoft Docs
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
ms.openlocfilehash: 98db9c92f682808ce8ecc9f6aa382a2eb2bd8495
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786257"
---
# <a name="isimpleconnectionpointadvise"></a>ISimpleConnectionPoint::Advise
建立简单连接点对象和客户端的接收器之间的连接。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Advise(  
   IDispatch*  pdisp,  
   DWORD*      pdwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdisp`  
 [in]指向`IDispatch`接口在客户端上的通知接收器。 客户端的接收器从简单的连接点接收传出调用。  
  
 `pdwCookie`  
 [out]指向返回的令牌，用于唯一标识此连接。 调用方在更高版本使用此令牌来将其传递到删除连接`ISimpleConnectionPoint::Unadvise`方法。 如果未成功建立连接，此值为零。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法会建立简单连接点对象和客户端的接收器之间的连接。  
  
## <a name="see-also"></a>请参阅  
 [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)   
 [ISimpleConnectionPoint::Unadvise](../../winscript/reference/isimpleconnectionpoint-unadvise.md)