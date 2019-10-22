---
title: IDebugApplicationNodeEvents：： onDetach |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationNodeEvents.onDetach
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugApplicationNodeEvents::onDetach
ms.assetid: ef0cbe40-8c52-4bc9-bed0-9fc508abec6e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bb1a33cbec8ef032c1c4fedba28ad4013e676f0d
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574682"
---
# <a name="idebugapplicationnodeeventsondetach"></a>IDebugApplicationNodeEvents::onDetach
处理一个事件，该事件表明调试应用程序节点对象已从父节点分离。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onDetach();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法处理一个事件，该事件表明调试应用程序节点对象已从父节点分离。  
  
 @No__t_0 接口的实施者引发此事件。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNodeEvents 接口](../../winscript/reference/idebugapplicationnodeevents-interface.md)   
 [IDebugApplicationNodeEvents：： onAttach](../../winscript/reference/idebugapplicationnodeevents-onattach.md)    
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)