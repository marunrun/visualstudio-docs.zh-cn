---
title: IDispatchEx::GetMemberName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetMemberName
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetMemberName method
ms.assetid: 5e59b63c-b781-4b90-88fd-40603a379a2d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 155c8db6e772460ae8ad4e8b5a70ae5e67b49ec1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000876"
---
# <a name="idispatchexgetmembername"></a>IDispatchEx::GetMemberName
检索成员的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetMemberName(  
   DISPID id,  
   BSTR *pbstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `id`  
 标识成员。 使用`GetDispID`或`GetNextDispID`若要获取的调度标识符。  
  
 `pbstrName`  
 地址`BSTR`，它接收的成员的名称。 调用应用程序负责释放此值。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`DISP_E_UNKNOWNNAME`|不知道名称。|  
  
## <a name="example"></a>示例  
  
```cpp
HRESULT hr;  
   BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;  
  
   // Assign to pdex  
   hr = pdex->GetNextDispID(fdexEnumAll, DISPID_STARTENUM, &dispid);  
   while (hr == NOERROR)  
   {  
      hr = pdex->GetMemberName(dispid, &bstrName);  
      if (!wcscmp(bstrName, OLESTR("Bar")))  
      {  
         SysFreeString(bstrName);  
         return TRUE;  
      }  
   SysFreeString(bstrName);  
   hr = pdex->GetNextDispID(fdexEnumAll, dispid, &dispid);  
   }  
```  
  
## <a name="see-also"></a>请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)