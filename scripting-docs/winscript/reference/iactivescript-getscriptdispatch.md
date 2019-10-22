---
title: IActiveScript：： GetScriptDispatch |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptDispatch
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptDispatch
ms.assetid: 2092ccd4-1f4c-493a-b5b7-077a70ce95ca
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba53f2eccde18bd5b2d9c609ea680b50cb7261c9
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575752"
---
# <a name="iactivescriptgetscriptdispatch"></a>IActiveScript::GetScriptDispatch
检索与当前正在运行的脚本相关联的方法和属性的 `IDispatch` 接口。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptDispatch(  
    LPCOLESTR pstrItemName  // address of item name  
    IDispatch **ppdisp      // receives IDispatch pointer  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrItemName`  
 中缓冲区的地址，该缓冲区包含调用方为其提供关联调度对象的项的名称。 如果 `NULL` 此参数，则调度对象将包含该脚本定义的所有全局方法和属性作为其成员。 通过 `IDispatch` 接口和关联的 `ITypeInfo` 接口，主机可以调用脚本方法或查看和修改脚本变量。  
  
 `ppdisp`  
 弄变量的地址，该变量接收指向与脚本的全局方法和属性关联的对象的指针。 如果脚本引擎不支持此类对象，则会返回 `NULL`。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，尚未加载或初始化脚本引擎）。|  
|`S_FALSE`|脚本引擎不支持调度对象;`ppdisp` 参数设置为 NULL。|  
  
## <a name="remarks"></a>备注  
 由于方法和属性可以通过调用[IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)接口添加，因此此方法返回的 `IDispatch` 接口可以动态支持新的方法和属性。 同样，当添加方法和属性时，`IDispatch::GetTypeInfo` 方法应返回一个新的唯一 `ITypeInfo` 接口。 但请注意，语言引擎不得以与以前返回的任何 `ITypeInfo` 接口不兼容的方式更改 `IDispatch` 接口。 例如，这意味着，不会重复使用 Dispid。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)