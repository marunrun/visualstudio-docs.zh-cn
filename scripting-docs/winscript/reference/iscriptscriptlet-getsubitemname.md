---
title: IScriptScriptlet::GetSubItemName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptScriptlet.GetSubItemName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptScriptlet::GetSubItemName
ms.assetid: 9ad963fc-9ce8-4b77-92c1-fb90d6307801
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0c48517b7f9f5fab3250b8cff68ad288525145b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786792"
---
# <a name="iscriptscriptletgetsubitemname"></a>IScriptScriptlet::GetSubItemName
Scriptlet 的对象主机的完全限定名称中返回的最后一个标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSubItemName(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]如果主机的完全限定 scriptlet 的名称有多个级别，`pbstr`返回在第二个级别的标识符的缓冲区地址。  
  
 如果主机的完全限定 scriptlet 的名称有一个级别，`pbstr`返回在第一个级别的标识符的缓冲区地址。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptScriptlet 接口](../../winscript/reference/iscriptscriptlet-interface.md)