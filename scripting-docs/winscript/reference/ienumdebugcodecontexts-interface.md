---
title: IEnumDebugCodeContexts 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumDebugCodeContexts interface
ms.assetid: 47f17dc9-14bc-43c8-b874-00b5802076eb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4e90e19a4bd12dfeeeef1b8f5498f729aa076adb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951460"
---
# <a name="ienumdebugcodecontexts-interface"></a>IEnumDebugCodeContexts 接口
枚举文档上下文对应的代码上下文。  
  
 除了继承的方法之外`IUnknown`，则`IEnumDebugCodeContexts`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugCodeContexts::Next](../../winscript/reference/ienumdebugcodecontexts-next.md)|检索指定的数目的枚举序列中的段。|  
|[IEnumDebugCodeContexts::Skip](../../winscript/reference/ienumdebugcodecontexts-skip.md)|将跳过枚举序列中的指定的段数。|  
|[IEnumDebugCodeContexts::Reset](../../winscript/reference/ienumdebugcodecontexts-reset.md)|将枚举序列重置到开头。|  
|[IEnumDebugCodeContexts::Clone](../../winscript/reference/ienumdebugcodecontexts-clone.md)|创建一个包含与当前枚举数相同的状态的枚举器。|