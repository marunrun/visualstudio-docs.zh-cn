---
title: IScriptEntry：： GetItemName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetItemName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetItemName
ms.assetid: 8f2562f1-8231-4a39-ad79-074f9ec3d403
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dcd1b83fa6d22fafc2123645f1f252fa1325f7f1
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575455"
---
# <a name="iscriptentrygetitemname"></a>IScriptEntry::GetItemName
返回标识 `IScriptEntry` 对象的项名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetItemName(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 弄包含项名称的缓冲区的地址。 项名称由主机用于标识该项。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 对于 `IScriptScriptlet` 对象，您可以使用[IActiveScriptAuthor：： AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md)设置项名称。 对于其他接口，可以使用[IScriptEntry：： SetItemName](../../winscript/reference/iscriptentry-setitemname.md)设置项名称。  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)