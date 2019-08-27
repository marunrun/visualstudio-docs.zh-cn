---
title: IScriptEntry::GetItemName | Microsoft Docs
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
ms.openlocfilehash: 9d8abc6d1264ce532adcbc59c262510a39ea7a91
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787851"
---
# <a name="iscriptentrygetitemname"></a>IScriptEntry::GetItemName
返回标识的项名称`IScriptEntry`对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetItemName(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]包含的项名称的缓冲区的地址。 主机使用的项名称来标识该项。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 有关`IScriptScriptlet`对象，通过设置项目名称[IActiveScriptAuthor::AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md)。 对于其他接口，设置项名称使用[IScriptEntry::SetItemName](../../winscript/reference/iscriptentry-setitemname.md)。  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)