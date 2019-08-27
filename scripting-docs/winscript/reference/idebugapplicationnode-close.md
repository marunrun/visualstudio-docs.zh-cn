---
title: IDebugApplicationNode::Close | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationNode.Close
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplicationNode::Close
ms.assetid: ea8db480-2344-4c7b-960c-4fa97fa6c1b7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c634fd154c2470b1a154e5d1c9e97419a2e2e2b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990514"
---
# <a name="idebugapplicationnodeclose"></a>IDebugApplicationNode::Close
使此应用程序释放所有引用并进入非活动状态。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Close();  
```  
  
#### <a name="parameters"></a>参数  
 此方法需要任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 通常情况下，应用程序所有者应用程序退出时调用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)