---
title: IDispatchEx::DeleteMemberByDispID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.DeleteMemberByDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- DeleteMemberByDispID method
ms.assetid: f61231e5-ba93-4ac3-bde8-d363548356b3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 36eeeb4c28286bb5712be3908b47a5145e460597
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000939"
---
# <a name="idispatchexdeletememberbydispid"></a>IDispatchEx::DeleteMemberByDispID
删除成员的 DISPID。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT DeleteMemberByDispID(  
    DISPID id  
);  
```  
  
#### <a name="parameters"></a>参数  
 `id`  
 成员标识符。 使用`GetDispID`或`GetNextDispID`若要获取的调度标识符。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`S_FALSE`|成员存在，但不能删除。|  
  
## <a name="remarks"></a>备注  
 如果删除该成员，则需要保持有效，DISPID `GetNextDispID`。  
  
 如果删除具有给定名称的成员，并且以后重新创建具有相同名称的成员，DISPID 应相同。 （仅大小写不同的成员名称是否"相同"与对象相关。）  
  
## <a name="example"></a>示例  
  
```cpp
BSTR bstrName;  
DISPID dispid;  
IDispatchEx *pdex;   
  
// Assign to pdex and bstrName  
if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)))  
    pdex->DeleteMemberByDispID(dispid);  
```  
  
## <a name="see-also"></a>请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)