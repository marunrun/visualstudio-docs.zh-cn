---
title: IActiveScriptAuthor::RemoveNamedItem | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.RemoveNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::RemoveNamedItem
ms.assetid: 1173ef46-39a5-4bc1-8e0c-89259a16be16
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 052704b9a1bef8c50c457e51438f0204813c2efe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955138"
---
# <a name="iactivescriptauthorremovenameditem"></a>IActiveScriptAuthor::RemoveNamedItem
删除`NamedItem`脚本创作引擎的命名空间中的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT RemoveNamedItem(  
   LPCOLESTR          pszName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszName`  
 [in]标识的缓冲区的地址`NamedItem`要移除对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`S_FALSE`|`NamedItem`对象不存在脚本创作引擎的命名空间中。|  
  
## <a name="remarks"></a>备注  
 [Iactivescript:: Addnameditem](../../winscript/reference/iactivescript-addnameditem.md)用于注入`NamedItem`到脚本引擎的命名空间创作的对象。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::AddNamedItem](../../winscript/reference/iactivescriptauthor-addnameditem.md)