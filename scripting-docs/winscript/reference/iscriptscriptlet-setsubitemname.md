---
title: IScriptScriptlet::SetSubItemName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptScriptlet.SetSubItemName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptScriptlet::SetSubItemName
ms.assetid: 619f222f-b4c3-4c7b-9d19-e4e7037343a6
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8b9a4f67fb5a383666cb9f83fc2e0e38fbffb51f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786557"
---
# <a name="iscriptscriptletsetsubitemname"></a>IScriptScriptlet::SetSubItemName
Scriptlet 的对象主机的完全限定名称中设置的最后一个标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetSubItemName(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>参数  
 `psz`  
 如果主机的完全限定 scriptlet 的名称有多个级别，`psz`是在第二个级别的标识符的缓冲区地址。  
  
 如果主机的完全限定 scriptlet 的名称有一个级别，`psz`是在第一个级别的标识符的缓冲区地址。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptScriptlet 接口](../../winscript/reference/iscriptscriptlet-interface.md)