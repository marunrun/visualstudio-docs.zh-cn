---
title: IEnumRemoteDebugApplications 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IEnumRemoteDebugApplications interface
ms.assetid: ceb5fbe7-d131-4352-9dd1-af80acd3f3f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 430551002bc7603d86f9c7fb624ec438734bd766
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963245"
---
# <a name="ienumremotedebugapplications-interface"></a>IEnumRemoteDebugApplications 接口
枚举应用程序对象。 此接口可用于枚举在"附加到应用程序"对话框中的计算机上运行的应用程序。  
  
 除了继承的方法之外`IUnknown`，则`IEnumRemoteDebugApplications`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IEnumRemoteDebugApplications::Clone](../../winscript/reference/ienumremotedebugapplications-clone.md)|创建一个包含与当前枚举数相同的状态的枚举器。|  
|[IEnumRemoteDebugApplications::Next](../../winscript/reference/ienumremotedebugapplications-next.md)|检索指定的数目的枚举序列中的段。|  
|[IEnumRemoteDebugApplications::Reset](../../winscript/reference/ienumremotedebugapplications-reset.md)|将枚举序列重置到开头。|  
|[IEnumRemoteDebugApplications::Skip](../../winscript/reference/ienumremotedebugapplications-skip.md)|将跳过枚举序列中的指定的段数。|