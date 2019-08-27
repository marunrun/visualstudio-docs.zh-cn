---
title: IDispatchEx::GetNameSpaceParent |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetNameSpaceParent
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetNameSpaceParent method
ms.assetid: 0b077d39-2fd6-4390-8cd5-128d9b8dc90c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1abe2a880e12d6a4a3c1dfda32d30722525858f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000821"
---
# <a name="idispatchexgetnamespaceparent"></a>IDispatchEx::GetNameSpaceParent
检索命名空间对象的父对象的接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetNameSpaceParent(  
   IUnknown **ppunk  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppunk`  
 地址`IUnknown`接收命名空间父接口的接口指针。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，则或 OLE 定义的错误代码，否则为。  
  
## <a name="see-also"></a>请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)