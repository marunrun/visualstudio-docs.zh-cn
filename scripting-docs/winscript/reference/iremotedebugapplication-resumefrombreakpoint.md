---
title: IRemoteDebugApplication::ResumeFromBreakPoint | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplication.ResumeFromBreakPoint
apilocation:
- pdm.dll
helpviewer_keywords:
- IRemoteDebugApplication::ResumeFromBreakPoint
ms.assetid: a613cc2b-1d69-4713-a235-64372c253b4a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5844381188cb03c99ab0a44ed9b9e0fdbab67e6e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944174"
---
# <a name="iremotedebugapplicationresumefrombreakpoint"></a>IRemoteDebugApplication::ResumeFromBreakPoint
继续当前断点的应用程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT ResumeFromBreakPoint(  
   IRemoteDebugApplicationThread*  prptFocus,  
   BREAKRESUMEACTION               bra,  
   ERRORRESUMEACTION               era  
);  
```  
  
#### <a name="parameters"></a>参数  
 `prptFocus`  
 [in]单步执行模式，这是受到影响的单步执行模式的线程。  
  
 `bra`  
 [in]要在恢复应用程序时执行的操作。  
  
 `era`  
 [in]要在应用程序因出错而停止的情况下执行的操作。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法将继续当前断点的应用程序。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)   
 [BREAKRESUMEACTION 枚举](../../winscript/reference/breakresumeaction-enumeration.md)   
 [ERRORRESUMEACTION 枚举](../../winscript/reference/errorresumeaction-enumeration.md)