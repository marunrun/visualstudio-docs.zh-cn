---
title: IActiveScriptStats 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptStats interface
ms.assetid: dbe84d6f-1b77-4877-aced-cd4e01ead5b5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e7a0e1e616fdee2dac58c8a5a1d24ed120b28bc2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991978"
---
# <a name="iactivescriptstats-interface"></a>IActiveScriptStats 接口
使宿主可以查询正在运行的脚本的统计信息。 主机可以使用此信息以确定是否脚本具有执行操作太长时间才能完成。  
  
 除了继承的方法之外`IUnknown`，则`IActiveScriptStats`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptStats::GetStat](../../winscript/reference/iactivescriptstats-getstat.md)|返回一个标准脚本统计信息。|  
|[IActiveScriptStats::GetStatEx](../../winscript/reference/iactivescriptstats-getstatex.md)|返回自定义脚本统计信息。|  
|[IActiveScriptStats::ResetStats](../../winscript/reference/iactivescriptstats-resetstats.md)|重置此脚本的统计信息。|