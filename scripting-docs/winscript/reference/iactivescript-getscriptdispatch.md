---
title: 'Iactivescript:: Getscriptdispatch |Microsoft Docs'
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
ms.openlocfilehash: c329a4dbf42461369441b86f6d9ba18992916366
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935592"
---
# <a name="iactivescriptgetscriptdispatch"></a>IActiveScript::GetScriptDispatch
检索`IDispatch`接口的方法和属性与当前正在运行的脚本相关联。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptDispatch(  
    LPCOLESTR pstrItemName  // address of item name  
    IDispatch **ppdisp      // receives IDispatch pointer  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrItemName`  
 [in]包含为其调用方需要关联的调度对象的项的名称的缓冲区的地址。 如果此参数为`NULL`，调度对象包含作为其成员的所有全局方法和属性定义的脚本。 通过`IDispatch`接口和关联`ITypeInfo`接口，主机可以调用脚本方法或查看和修改脚本变量。  
  
 `ppdisp`  
 [out]接收指向与脚本的全局方法和属性关联的对象的变量的地址。 如果脚本引擎不支持此类对象，`NULL`返回。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
|`S_FALSE`|脚本引擎不支持的调度对象;`ppdisp`参数设置为 NULL。|  
  
## <a name="remarks"></a>备注  
 因为可以通过调用添加方法和属性[IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)接口，`IDispatch`新方法和属性，可以动态地支持此方法返回的接口。 同样，`IDispatch::GetTypeInfo`方法应返回一个新唯一`ITypeInfo`接口添加方法和属性时。 但是，请注意，语言引擎必须更改`IDispatch`接口中使用任何兼容方式是否以前`ITypeInfo`返回接口。 例如，这意味着，将永远不会重复 Dispid。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)