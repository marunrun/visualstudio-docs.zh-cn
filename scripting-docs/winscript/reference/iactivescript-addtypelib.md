---
title: IActiveScript::AddTypeLib | Microsoft Docs
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
ms.openlocfilehash: c4943d1305c2f25de4eec9e782949a66827de879
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955086"
---
# <a name="iactivescriptaddtypelib"></a>IActiveScript::AddTypeLib
将类型库添加到该脚本在命名空间。 它类似于`#include`指令在 C /C++。 它允许一组预定义项目类的定义，如`typedefs`，和命名的常量添加到可供脚本运行时环境。  
  
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
 [in]若要添加的类型库的 CLSID。  
  
 `dwMaj`  
 [in]主版本号。  
  
 `dwMin`  
 [in]次版本号。  
  
 `dwFlags`  
 [in]选项标志。 可以是以下值：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTYPELIB_ISCONTROL|类型库描述主机所使用的 ActiveX 控件。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
|`TYPE_E_CANTLOADLIBRARY`|无法加载指定的类型库。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)