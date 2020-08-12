---
title: IDispatchEx：:D eleteMemberByName |Microsoft Docs
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
ms.openlocfilehash: cf62972b192d73bd130d15066d79ea70fe24beb8
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144592"
---
# <a name="idispatchexdeletememberbyname"></a>IDispatchEx::DeleteMemberByName
按名称删除成员。  
  
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
 确定成员名称是否区分大小写。 这可以是以下值之一：  
  
|值|含义|  
|-----------|-------------|  
|fdexNameCaseSensitive|请求以区分大小写的方式进行名称查找。 对于不支持区分大小写的查找的对象，可将其忽略。|  
|fdexNameCaseInsensitive|请求以不区分大小写的方式进行名称查找。 对于不支持不区分大小写的查找的对象，可将其忽略。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|值|含义|
|-|-|  
|`S_OK`|成功。|  
|`S_FALSE`|成员存在，但不能删除。|  
  
## <a name="remarks"></a>备注  
 如果删除了成员，DISPID 需要对有效 `GetNextDispID` 。  
  
 如果删除具有给定名称的成员，然后重新创建同名的成员，则 DISPID 应相同。  (是否只有大小写不同的成员才是依赖于对象的成员。 )   
  
## <a name="example"></a>示例  
  
```cpp
BSTR bstrName;  
IDispatchEx *pdex;  
  
// Assign to pdex and bstrName  
pdex->DeleteMemberByName(bstrName, fdexNameCaseSensitive);  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)