---
title: IScriptScriptlet::GetSimpleEventName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptScriptlet. GetSimpleEventName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptScriptlet::GetSimpleEventName
ms.assetid: 012eb555-b26c-4248-bbcc-fc30e6f2b308
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e767c260dcdda2d92a7d90f7fd12af6918ac16d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786884"
---
# <a name="iscriptscriptlet-getsimpleeventname"></a>IScriptScriptlet::GetSimpleEventName
返回与 scriptlet 相关联的简单事件名称。 这是不包含任何空白区域的单个词名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSimpleEventName(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]包含与之关联的简单事件名称的缓冲区`IScriptScriptlet`对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptScriptlet 接口](../../winscript/reference/iscriptscriptlet-interface.md)