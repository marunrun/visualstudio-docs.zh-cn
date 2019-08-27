---
title: IRemoteDebugApplicationThread::EnumStackFrames |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationThread.EnumStackFrames
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplicationThread::EnumStackFrames
ms.assetid: 605ce83d-43d2-47ea-b066-ec8f0da50ca6
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 96ca35779ea9f113fc96e485f028f1e74058990a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788443"
---
# <a name="iremotedebugapplicationthreadenumstackframes"></a>IRemoteDebugApplicationThread::EnumStackFrames
返回与此线程的堆栈帧的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumStackFrames(  
   IEnumDebugStackFrames**  ppedsf  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppedsf`  
 [out]与此线程的堆栈帧的一个枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 断点中，必须从调用此方法。 堆栈帧枚举器应返回的帧的堆栈顶部开始从最新入栈帧开始。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplicationThread 接口](../../winscript/reference/iremotedebugapplicationthread-interface.md)