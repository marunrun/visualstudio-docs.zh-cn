---
title: IEnumDebugStackFrames Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumDebugStackFrames interface
ms.assetid: 13484429-0140-4f4f-8502-3ca2a0553ed4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 224c26bccc5443cb20e2ca514ac6df1a111df05e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963359"
---
# <a name="ienumdebugstackframes-interface"></a>IEnumDebugStackFrames 接口
枚举的线程对应的堆栈帧。  
  
## <a name="methods"></a>方法  
 除了继承的方法之外`IUnknown`，则`IEnumDebugStackFrames`接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugStackFrames::Next](../../winscript/reference/ienumdebugstackframes-next.md)|检索指定的数目的枚举序列中的段。|  
|[IEnumDebugStackFrames::Skip](../../winscript/reference/ienumdebugstackframes-skip.md)|将跳过枚举序列中的指定的段数。|  
|[IEnumDebugStackFrames::Reset](../../winscript/reference/ienumdebugstackframes-reset.md)|将枚举序列重置到开头。|  
|[IEnumDebugStackFrames::Clone](../../winscript/reference/ienumdebugstackframes-clone.md)|创建一个包含与当前枚举数相同的状态的枚举器。|