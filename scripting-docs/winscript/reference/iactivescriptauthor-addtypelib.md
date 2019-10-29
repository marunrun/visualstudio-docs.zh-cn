---
title: IActiveScriptAuthor：： AddTypeLib |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.AddTypeLib
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::AddTypeLib
ms.assetid: d6696547-3eb5-4f31-9c5c-60aa29b6f083
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0f4bbcc694b24ffafd4333f635c7cdf0c67793a7
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985340"
---
# <a name="iactivescriptauthoraddtypelib"></a>IActiveScriptAuthor::AddTypeLib
将类型库添加到脚本的命名空间中。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddTypeLib(  
   REFGUID   rguidTypeLib,  
   DWORD     dwMajor,  
   DWORD     dwMinor,  
   DWORD     dwFlags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `rguidTypeLib`  
 中要添加的类型库的 CLSID （类标识符）。  
  
 `dwMajor`  
 中主版本号。  
  
 `dwMinor`  
 中次版本号。  
  
 `dwFlags`  
 中不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法调用 `LoadTypeLib` 以加载类型库。 成功后，此方法将调用 `IActiveScriptAuthor::AddNamedItem` 以添加类型信息。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor：： AddNamedItem](../../winscript/reference/iactivescriptauthor-addnameditem.md)    
 [LoadTypeLib](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-loadtypelib)