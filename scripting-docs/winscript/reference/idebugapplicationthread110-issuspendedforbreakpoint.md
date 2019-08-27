---
title: IDebugApplicationThread110::IsSuspendedForBreakPoint |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThread110::IsSuspendedForBreakPoint
ms.assetid: 60688222-557f-4a43-a19b-846cee393cd0
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 82b8957ae9f2b6674af7addf2239c745115e4e3f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440527"
---
# <a name="idebugapplicationthread110issuspendedforbreakpoint"></a>IDebugApplicationThread110::IsSuspendedForBreakPoint
确定是否[IDebugApplicationThreadEvents110::OnSuspendForBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onsuspendforbreakpoint.md)已在此线程上调用，但尚未完成。  
  
> [!IMPORTANT]
> [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT IsSuspendedForBreakPoint([out, annotation("_Out_")] BOOL * pfIsSuspended);  
```  
  
#### <a name="parameters"></a>参数  
 `pfIsSuspended`  
 [out]`true`如果针对某个断点，否则会挂起线程`false`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationThread110 接口](../../winscript/reference/idebugapplicationthread110-interface.md)