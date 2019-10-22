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
ms.openlocfilehash: 57f0faf6004e2219600f0dbd63749a7e65ca438c
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576602"
---
# <a name="idispatchexgetdispid"></a>IDispatchEx::GetDispID
将单个成员名称映射到其相应的 DISPID，然后可以在后续调用 `IDispatchEx::InvokeEx` 时使用该名称。  
  
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
|fdexNameCaseSensitive|请求以区分大小写的方式进行名称查找。 对于不支持区分大小写的查找的对象，可能会被忽略。|  
|fdexNameEnsure|请求创建成员（如果尚未存在）。 应为新成员创建值 `VT_EMPTY`。|  
|fdexNameImplicit|指示当未显式指定基对象时，调用方正在搜索特定名称的成员的对象。|  
|fdexNameCaseInsensitive|请求以不区分大小写的方式进行名称查找。 对于不支持不区分大小写的查找的对象，可能会被忽略。|  
  
 `pid`  
 指向调用方分配的用于接收 DISPID 结果的位置的指针。 如果发生错误，`pid` 包含 DISPID_UNKNOWN。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|`E_OUTOFMEMORY`|内存不足。|  
|`DISP_E_UNKNOWNNAME`|名称未知。|  
  
## <a name="remarks"></a>备注  
 可以使用 `GetDispID` 而不是 `GetIDsOfNames` 来获取给定成员的 DISPID。  
  
 由于 `IDispatchEx` 允许添加和删除成员，因此在对象的生存期内，Dispid 集不会保持不变。  
  
 @No__t_1 中未使用的 `riid` 参数已被移除。  
  
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