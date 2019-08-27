---
title: IEnumDebugApplicationNodes Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumDebugApplicationNodes interface
ms.assetid: 4fd38b44-3f9a-4d23-9a8f-7dc98f72725f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d23f8a8eaa8e10c503d7ec73f4cd5d4f6ea24404
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951731"
---
# <a name="ienumdebugapplicationnodes-interface"></a>IEnumDebugApplicationNodes 接口
枚举与应用程序关联的节点的子节点。  
  
 除了继承的方法之外`IUnknown`，则`IEnumDebugApplicationNodes`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumDebugApplicationNodes::Next](../../winscript/reference/ienumdebugapplicationnodes-next.md)|检索指定的数目的枚举序列中的段。|  
|[IEnumDebugApplicationNodes::Skip](../../winscript/reference/ienumdebugapplicationnodes-skip.md)|将跳过枚举序列中的指定的段数。|  
|[IEnumDebugApplicationNodes::Reset](../../winscript/reference/ienumdebugapplicationnodes-reset.md)|将枚举序列重置到开头。|  
|[IEnumDebugApplicationNodes::Clone](../../winscript/reference/ienumdebugapplicationnodes-clone.md)|创建一个包含与当前枚举数相同的状态的枚举器。|