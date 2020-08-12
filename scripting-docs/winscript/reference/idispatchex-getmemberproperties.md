---
title: IDispatchEx：： GetMemberProperties |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetMemberProperties
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetMemberProperties method
ms.assetid: 20d43209-12e2-472a-9bf3-81eced137b71
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 488f8790ec25532fb611f18e8b24e7e7dba2e2f4
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144542"
---
# <a name="idispatchexgetmemberproperties"></a>IDispatchEx::GetMemberProperties
检索成员的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetMemberProperties(  
   DISPID id,  
   DWORD grfdexFetch,  
   DWORD *pgrfdex  
);  
```  
  
#### <a name="parameters"></a>参数  
 `id`  
 标识成员。 使用 `GetDispID` 或 `GetNextDispID` 获取调度标识符。  
  
 `grfdexFetch`  
 确定要检索的属性。 这可以是下列值的组合 `pgrfdex` ：和/或下列值的组合：  
  
|值|含义|  
|-----------|-------------|  
|grfdexPropCanAll|结合了 fdexPropCanGet、fdexPropCanPut、fdexPropCanPutRef、fdexPropCanCall、fdexPropCanConstruct 和 fdexPropCanSourceEvents。|  
|grfdexPropCannotAll|结合了 fdexPropCannotGet、fdexPropCannotPut、fdexPropCannotPutRef、fdexPropCannotCall、fdexPropCannotConstruct 和 fdexPropCannotSourceEvents。|  
|grfdexPropExtraAll|将 fdexPropNoSideEffects 和 fdexPropDynamicType 组合在一起。|  
|grfdexPropAll|结合了 grfdexPropCanAll、grfdexPropCannotAll 和 grfdexPropExtraAll。|  
  
 `pgrfdex`  
 接收请求的属性的的地址 `DWORD` 。 这可以是以下值的组合：  
  
|值|含义|  
|-----------|-------------|  
|fdexPropCanGet|可以使用 DISPATCH_PROPERTYGET 获取此成员。|  
|fdexPropCannotGet|无法使用 DISPATCH_PROPERTYGET 获取此成员。|  
|fdexPropCanPut|可以使用 DISPATCH_PROPERTYPUT 设置成员。|  
|fdexPropCannotPut|该成员不能使用 DISPATCH_PROPERTYPUT 设置。|  
|fdexPropCanPutRef|可以使用 DISPATCH_PROPERTYPUTREF 设置成员。|  
|fdexPropCannotPutRef|该成员不能使用 DISPATCH_PROPERTYPUTREF 设置。|  
|fdexPropNoSideEffects|该成员没有副作用。 例如，调试器可以安全地获取/设置/调用此成员，而无需更改正在调试的脚本的状态。|  
|fdexPropDynamicType|该成员是动态的，并且可以在对象的生存期内更改。|  
|fdexPropCanCall|成员可以使用 DISPATCH_METHOD 作为方法进行调用。|  
|fdexPropCannotCall|不能使用 DISPATCH_METHOD 将成员作为方法进行调用。|  
|fdexPropCanConstruct|可以使用 DISPATCH_CONSTRUCT 将成员作为构造函数进行调用。|  
|fdexPropCannotConstruct|不能使用 DISPATCH_CONSTRUCT 将成员作为构造函数进行调用。|  
|fdexPropCanSourceEvents|成员可以激发事件。|  
|fdexPropCannotSourceEvents|成员无法激发事件。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|值|含义|
|-|-|  
|`S_OK`|成功。|  
|`DISP_E_UNKNOWNNAME`|名称未知。|  
  
## <a name="example"></a>示例  
  
```cpp
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
   DWORD dwProps;  
  
   // Assign to pdex and bstrName  
   if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)) &&  
      SUCCEEDED(pdex->GetMemberProperties(dispid, grfdexPropAll, &dwProps)) &&  
         (dwProps & fdexPropCanPut))  
   {  
      // Assign to member  
   }  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx：： GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)