---
title: IDebugApplicationThreadEvents110::OnThreadRequestComplete | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThreadEvents110::OnThreadRequestComplete
ms.assetid: 7cdd73f3-d78e-4e2f-a204-7a1c45366b87
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5542d524506410e0a69dcb5addb6a7fe59209073
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440462"
---
# <a name="idebugapplicationthreadevents110onthreadrequestcomplete"></a>IDebugApplicationThreadEvents110::OnThreadRequestComplete
调用到使用 PDM 的线程的线程切换已完成。  
  
> [!IMPORTANT]
> [IDebugApplicationThreadEvents110 接口](../../winscript/reference/idebugapplicationthreadevents110-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT OnThreadRequestComplete( void );  
```  
  
#### <a name="parameters"></a>参数  
 此方法没有任何参数。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationThreadEvents110 接口](../../winscript/reference/idebugapplicationthreadevents110-interface.md)