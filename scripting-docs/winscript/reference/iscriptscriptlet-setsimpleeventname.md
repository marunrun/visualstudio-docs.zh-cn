---
title: IScriptScriptlet::SetSimpleEventName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptScriptlet.SetSimpleEventName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptScriptlet::SetSimpleEventName
ms.assetid: 7de9132e-635f-45df-9c92-83a24242b477
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 63e6d05066d59e14a7036fb8f371c9c20b886df7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786623"
---
# <a name="iscriptscriptletsetsimpleeventname"></a>IScriptScriptlet::SetSimpleEventName
设置与 scriptlet 相关联的简单事件名称。 这是不包含任何空白区域的单个词名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetSimpleEventName(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>参数  
 `psz`  
 [in]包含与之关联的简单事件名称的缓冲区`IScriptScriptlet`对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptScriptlet 接口](../../winscript/reference/iscriptscriptlet-interface.md)