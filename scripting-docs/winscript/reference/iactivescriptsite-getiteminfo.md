---
title: IActiveScriptSite：： GetItemInfo |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.GetItemInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_GetItemInfo
ms.assetid: f859ed3b-02c1-4924-99f8-5f5bf1bf8405
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3c0458f42466a264c30a440b1b14a028a2457f12
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570927"
---
# <a name="iactivescriptsitegetiteminfo"></a>IActiveScriptSite::GetItemInfo
允许脚本引擎获取使用[IActiveScript：： AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)方法添加的项的相关信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetItemInfo(  
    LPCOLESTR pstrName,     // address of item name  
    DWORD dwReturnMask,     // bit mask for information retrieval  
    IUnknown **ppunkItem,   // address of pointer to item's IUnknown  
    ITypeInfo **ppTypeInfo  // address of pointer to item's ITypeInfo  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrName`  
 中与项关联的名称，如[IActiveScript：： AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)方法中所指定。  
  
 `dwReturnMask`  
 中一个位掩码，指定应返回的有关项的信息。 脚本引擎应该请求尽可能少的信息量，因为某些返回参数（例如 `ITypeInfo`）可能需要相当长的时间来加载或生成。 可以是以下值的组合：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTINFO_IUNKNOWN|返回此项的 `IUnknown` 接口。|  
|SCRIPTINFO_ITYPEINFO|返回此项的 `ITypeInfo` 接口。|  
  
 `ppunkItem`  
 弄变量的地址，该变量接收指向与给定项关联的 `IUnknown` 接口的指针。 脚本引擎可以使用 `IUnknown::QueryInterface` 方法获取该项的 `IDispatch` 接口。 如果 `dwReturnMask` 不包含 SCRIPTINFO_IUNKNOWN 值，则此参数将接收 NULL。 此外，如果没有与项名称关联的对象，则它将接收 NULL;此机制用于在使用[IActiveScript：： AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md)方法中设置的 SCRIPTITEM_CODEONLY 标志添加命名项时创建一个简单类。  
  
 `ppTypeInfo`  
 弄变量的地址，该变量接收指向与项关联的 `ITypeInfo` 接口的指针。 如果 `dwReturnMask` 不包含 SCRIPTINFO_ITYPEINFO 值，或者类型信息对此项不可用，则此参数将接收 NULL。 如果类型信息不可用，则对象不能源事件，并且必须使用 `IDispatch::GetIDsOfNames` 方法实现名称绑定。 请注意，检索到的 `ITypeInfo` 接口描述项的 coclass （TKIND_COCLASS），因为该对象可能支持多个接口和事件接口。 如果项支持 `IProvideMultipleTypeInfo` 接口，则检索到的 `ITypeInfo` 接口与将使用 `IProvideMultipleTypeInfo::GetInfoOfIndex` 方法获取的索引零 `ITypeInfo` 相同。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`TYPE_E_ELEMENTNOTFOUND`|找不到指定名称的项。|  
  
## <a name="remarks"></a>备注  
 此方法仅检索 `dwReturnMask` 参数指示的信息;这可以提高性能。 例如，如果某个项不需要 `ITypeInfo` 接口，则未在 `dwReturnMask` 中指定它。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)