---
title: IScriptScriptlet::GetEventName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptScriptlet.GetEventName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptScriptlet::GetEventName
ms.assetid: 548fa650-808e-4c96-8253-5c72e67e8215
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 56566c85aed88faadf740392ad3ec06aa848431e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786752"
---
# <a name="iscriptscriptletgeteventname"></a>IScriptScriptlet::GetEventName
返回与 scriptlet 相关联的事件的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetEventName(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]包含与之关联的事件名称的缓冲区`IScriptScriptlet`对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptScriptlet 接口](../../winscript/reference/iscriptscriptlet-interface.md)