---
title: IDispatchEx：： GetDispID |Microsoft Docs
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
ms.openlocfilehash: 81bb33a1e793f38e15dc51b37c4fa062eb54e7fa
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144528"
---
# <a name="idispatchexgetdispid"></a>IDispatchEx::GetDispID
将单个成员名称映射到它的相应 DISPID，然后在对的后续调用中使用该名称 `IDispatchEx::InvokeEx` 。  
  
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
  
|值|含义|  
|-----------|-------------|  
|fdexNameCaseSensitive|请求以区分大小写的方式进行名称查找。 对于不支持区分大小写的查找的对象，可能会被忽略。|  
|fdexNameEnsure|请求创建成员（如果尚未存在）。 应该用值创建新成员 `VT_EMPTY` 。|  
|fdexNameImplicit|指示在未显式指定基对象时，调用方正在搜索特定名称的成员的对象 (s) 。|  
|fdexNameCaseInsensitive|请求以不区分大小写的方式进行名称查找。 对于不支持不区分大小写的查找的对象，可能会被忽略。|  
  
 `pid`  
 指向调用方分配的用于接收 DISPID 结果的位置的指针。 如果发生错误，则 `pid` 包含 DISPID_UNKNOWN。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|值|含义|
|-|-|  
|`S_OK`|成功。|  
|`E_OUTOFMEMORY`|内存不足。|  
|`DISP_E_UNKNOWNNAME`|名称未知。|  
  
## <a name="remarks"></a>备注  
 `GetDispID`可以使用而不是 `GetIDsOfNames` 来获取给定成员的 DISPID。  
  
 由于 `IDispatchEx` 允许添加和删除成员，因此在对象的生存期内，dispid 集不会保持不变。  
  
 中未使用的 `riid` 参数已 `IDispatch::GetIDsOfNames` 被移除。  
  
## <a name="example"></a>示例  
  
```cpp
BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;   
  
   // Assign to pdex and bstrName  
   pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid);  
   // Use dispid  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)