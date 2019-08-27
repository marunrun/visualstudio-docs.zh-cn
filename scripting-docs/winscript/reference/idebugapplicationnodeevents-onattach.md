---
title: IDebugApplicationNodeEvents::onAttach | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplicationNodeEvents.onAttach
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugApplicationNodeEvents::onAttach
ms.assetid: b610c7e4-1c96-47ee-958e-3a1f5f621af3
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d606292eda60fbb367802dbd5df973b933f3fe14
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821950"
---
# <a name="idebugapplicationnodeeventsonattach"></a>IDebugApplicationNodeEvents::onAttach
处理以表明调试应用程序节点对象已附加到父节点的事件。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT onAttach(  
   IDebugApplicationNode*  prddpParent  
);  
```  
  
#### <a name="parameters"></a>参数  
 `prddpParent`  
 [in]调试应用程序节点的此节点的父级。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法处理表明调试应用程序节点对象已附加到父节点的事件。  
  
 实施者`IDebugApplicationNode`接口引发此事件。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNodeEvents 接口](../../winscript/reference/idebugapplicationnodeevents-interface.md)   
 [IDebugApplicationNodeEvents::onDetach](../../winscript/reference/idebugapplicationnodeevents-ondetach.md)   
 [IDebugApplicationNode 接口](../../winscript/reference/idebugapplicationnode-interface.md)