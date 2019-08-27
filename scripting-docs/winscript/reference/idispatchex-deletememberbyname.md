---
title: IDispatchEx::DeleteMemberByName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.DeleteMemberByName
apilocation:
- scrobj.dll
helpviewer_keywords:
- DeleteMemberByName method
ms.assetid: a01b4e6a-d989-4b29-bb3f-04554f8c39f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dc7c8db4ab28e0bd0fcb48f352cb07595f72fd17
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000885"
---
# <a name="idispatchexdeletememberbyname"></a>IDispatchEx::DeleteMemberByName
按名称删除一个成员。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT DeleteMemberByName(  
   BSTR bstrName,  
   DWORD grfdex  
  
```  
  
#### <a name="parameters"></a>参数  
 `bstrName`  
 要删除的成员的名称。  
  
 `grfdex`  
 确定成员名称是否区分大小写。 这可以是下列值之一：  
  
|“值”|含义|  
|-----------|-------------|  
|fdexNameCaseSensitive|名称查找区分大小写的方式完成的请求。 可以忽略不支持区分大小写查找的对象。|  
|fdexNameCaseInsensitive|该名称查找可在不区分大小写的方式完成的请求。 可以忽略不支持不区分大小写查找的对象。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`S_FALSE`|成员存在，但不能删除。|  
  
## <a name="remarks"></a>备注  
 如果删除该成员，则需要保持有效，DISPID `GetNextDispID`。  
  
 如果删除具有给定名称的成员，并且以后重新创建具有相同名称的成员，DISPID 应相同。 （仅大小写不同的成员是否是"相同"与对象相关。）  
  
## <a name="example"></a>示例  
  
```cpp
BSTR bstrName;  
IDispatchEx *pdex;  
  
// Assign to pdex and bstrName  
pdex->DeleteMemberByName(bstrName, fdexNameCaseSensitive);  
```  
  
## <a name="see-also"></a>请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)