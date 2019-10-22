---
title: IActiveScript：： AddTypeLib |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.AddTypeLib
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_AddTypeLib
ms.assetid: 8e507ea8-c80a-471c-b482-ae753c6e8595
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 254a5133d42689020eaaae290a1016de4b848100
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575814"
---
# <a name="iactivescriptaddtypelib"></a>IActiveScript::AddTypeLib
将类型库添加到脚本的命名空间中。 这与 C/C++中的 `#include` 指令类似。 它允许将一组预定义项（如类定义、`typedefs` 和命名常量）添加到脚本可用的运行时环境。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddTypeLib(  
    REFGUID guidTypeLib,  // CLSID of type library  
    DWORD dwMaj,          // major version number  
    DWORD dwMin,          // minor version number  
    DWORD dwFlags         // option flags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `guidTypeLib`  
 中要添加的类型库的 CLSID。  
  
 `dwMaj`  
 中主要版本号。  
  
 `dwMin`  
 中次版本号。  
  
 `dwFlags`  
 中选项标志。 可以是以下各项：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTYPELIB_ISCONTROL|类型库描述主机使用的 ActiveX 控件。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，尚未加载或初始化脚本引擎）。|  
|`TYPE_E_CANTLOADLIBRARY`|无法加载指定的类型库。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)