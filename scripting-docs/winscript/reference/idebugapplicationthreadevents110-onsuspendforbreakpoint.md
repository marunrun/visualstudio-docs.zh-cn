---
title: IDebugApplicationThreadEvents110::OnSuspendForBreakPoint |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThreadEvents110::OnSuspendForBreakPoint
ms.assetid: 224245ac-2aa2-43ae-97ed-493afc3d0122
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a9e39af9784b139e935c271fca6db565136352cf
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440424"
---
# <a name="idebugapplicationthreadevents110onsuspendforbreakpoint"></a>IDebugApplicationThreadEvents110::OnSuspendForBreakPoint
确定线程是否已完全挂起断点并没有恢复正常执行。  
  
> [!IMPORTANT]
> [IDebugApplicationThreadEvents110 接口](../../winscript/reference/idebugapplicationthreadevents110-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT OnSuspendForBreakPoint( void );  
```  
  
#### <a name="parameters"></a>参数  
 此方法没有任何参数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationThreadEvents110 接口](../../winscript/reference/idebugapplicationthreadevents110-interface.md)