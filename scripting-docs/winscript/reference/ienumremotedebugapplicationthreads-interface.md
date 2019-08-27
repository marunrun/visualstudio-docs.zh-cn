---
title: IEnumRemoteDebugApplicationThreads 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumRemoteDebugApplicationThreads interface
ms.assetid: 4ae6f8ef-e7be-4e2d-9be4-e0cde0a70eb1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d57e945593641036bbfbbecc90b790251c12075f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807207"
---
# <a name="ienumremotedebugapplicationthreads-interface"></a>IEnumRemoteDebugApplicationThreads 接口
枚举应用程序中正在运行的线程。  
  
 除了继承的方法之外`IUnknown`，则`IEnumRemoteDebugApplicationThreads`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumRemoteDebugApplicationThreads::Next](../../winscript/reference/ienumremotedebugapplicationthreads-next.md)|检索指定的数目的枚举序列中的段。|  
|[IEnumRemoteDebugApplicationThreads::Skip](../../winscript/reference/ienumremotedebugapplicationthreads-skip.md)|将跳过枚举序列中的指定的段数。|  
|[IEnumRemoteDebugApplicationThreads::Reset](../../winscript/reference/ienumremotedebugapplicationthreads-reset.md)|将枚举序列重置到开头。|  
|[IEnumRemoteDebugApplicationThreads::Clone](../../winscript/reference/ienumremotedebugapplicationthreads-clone.md)|创建一个包含与当前枚举数相同的状态的枚举器。|