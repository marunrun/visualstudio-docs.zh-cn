---
title: ISimpleConnectionPoint::Unadvise | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISimpleConnectionPoint.Unadvise
apilocation:
- pdm.dll
helpviewer_keywords:
- ISimpleConnectionPoint::Unadvise
ms.assetid: eae06a58-ed42-4839-aad4-14420b15343f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 189c07c10e93df9a61218b6a94a0b317999676d2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001493"
---
# <a name="isimpleconnectionpointunadvise"></a>ISimpleConnectionPoint::Unadvise
终止先前通过建立的通知连接`ISimpleConnectionPoint::Advise`。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Unadvise(  
   DWORD  dwCookie  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwCookie`  
 [in]若要终止，从返回的连接令牌`ISimpleConnectionPoint::Advise`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 连接终止的通知连接时, 点调用`Release`期间连接的指针上的已保存方法`ISimpleConnectionPoint::Advise`方法。 调用反转`AddRef`的执行期间`ISimpleConnectionPoint::Advise`的连接点时调用的通知接收器`QueryInterface`。  
  
## <a name="see-also"></a>请参阅  
 [ISimpleConnectionPoint 接口](../../winscript/reference/isimpleconnectionpoint-interface.md)