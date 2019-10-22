---
title: IScriptEntry：： SetItemName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.SetItemName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::SetItemName
ms.assetid: 9551a7ec-38f8-466a-9722-09367763f380
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ba226704f5b064c86b52c1b349650d509b2b549
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575368"
---
# <a name="iscriptentrysetitemname"></a>IScriptEntry::SetItemName
设置标识 `IScriptEntry` 对象的项名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetItemName(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>参数  
 `psz`  
 中包含项名称的缓冲区的地址。 项名称由主机用于标识该项。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|方法未成功。|  
  
## <a name="remarks"></a>备注  
 对于 `IScriptEntry` 对象，此方法返回 `S_OK`。  
  
 对于 `IScriptScriptlet` 对象（从 `IScriptEntry` 派生），此方法返回 `E_FAIL`。 对于 `IScriptScriptlet` 对象，项名称由[IActiveScriptAuthor：： AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md)设置，不能更改。  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)   
 [IScriptEntry::GetItemName](../../winscript/reference/iscriptentry-getitemname.md)