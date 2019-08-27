---
title: IDispatchEx::GetDispID | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetDispID
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetDispID method
ms.assetid: a288d63d-b08a-4540-9d9d-0bcd182eff9a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 95ab1d72e5b2f608c51ac6e56be1986df8945ec2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000865"
---
# <a name="idispatchexgetdispid"></a>IDispatchEx::GetDispID
将单个成员名称映射到其相应的 DISPID，随后可在后续调用`IDispatchEx::InvokeEx`。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDispID(  
   BSTR bstrName,  
   DWORD grfdex,  
   DISPID *pid  
);  
```  
  
#### <a name="parameters"></a>参数  
 `bstrName`  
 传入要映射的名称。  
  
 `grfdex`  
 确定用于获取成员标识符的选项。 这可以是以下值的组合：  
  
|“值”|含义|  
|-----------|-------------|  
|fdexNameCaseSensitive|名称查找区分大小写的方式完成的请求。 可能会被忽略不支持区分大小写查找的对象。|  
|fdexNameEnsure|如果尚不存在的情况下创建成员的请求。 应使用的值创建新成员`VT_EMPTY`。|  
|fdexNameImplicit|指示未显式指定基对象时，调用方，对象搜索具有特定名称的成员。|  
|fdexNameCaseInsensitive|该名称查找可在不区分大小写的方式完成的请求。 可能会被忽略不支持不区分大小写查找的对象。|  
  
 `pid`  
 指向调用方分配的位置以接收 DISPID 结果的指针。 如果发生错误，`pid`包含 DISPID_UNKNOWN。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`E_OUTOFMEMORY`|内存不足。|  
|`DISP_E_UNKNOWNNAME`|不知道名称。|  
  
## <a name="remarks"></a>备注  
 `GetDispID` 可以使用而不是`GetIDsOfNames`获取的给定成员的 DISPID。  
  
 因为`IDispatchEx`允许添加和删除成员的 Dispid 集不会保持常量对象的生存期内。  
  
 未使用`riid`中的参数`IDispatch::GetIDsOfNames`已删除。  
  
## <a name="example"></a>示例  
  
```cpp
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
  
   // Assign to pdex and bstrName  
   pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid);  
   // Use dispid  
```  
  
## <a name="see-also"></a>请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)