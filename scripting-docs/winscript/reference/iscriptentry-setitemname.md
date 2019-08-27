---
title: IScriptEntry::SetItemName | Microsoft Docs
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
ms.openlocfilehash: d25ac4977f1fca44d63767c372db169f8cb61ea6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787653"
---
# <a name="iscriptentrysetitemname"></a>IScriptEntry::SetItemName
设置标识的项名称`IScriptEntry`对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetItemName(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>参数  
 `psz`  
 [in]包含的项名称的缓冲区的地址。 主机使用的项名称来标识该项。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|该方法未成功。|  
  
## <a name="remarks"></a>备注  
 有关`IScriptEntry`对象，此方法返回`S_OK`。  
  
 有关`IScriptScriptlet`对象 (从其派生`IScriptEntry`)，此方法返回`E_FAIL`。 有关`IScriptScriptlet`对象，通过设置项目名称[IActiveScriptAuthor::AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md) ，并且不能更改。  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)   
 [IScriptEntry::GetItemName](../../winscript/reference/iscriptentry-getitemname.md)