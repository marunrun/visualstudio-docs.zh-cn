---
title: ISetNextStatement 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b570c2e0-a173-4f14-97d8-f39465753115
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: de300a7af8492e6431f6b8513cde84a15895ad96
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786303"
---
# <a name="isetnextstatement-interface"></a>ISetNextStatement 接口
此接口由解释器以允许进程调试管理器更新当前语句实现。 从堆栈帧对象中，实现并 PDM 获取此接口通过 QueryInterface。  
  
 接口提供了可用于设置执行点，用于确定要执行的下一个语句的方法。  
  
 除了继承的方法之外`IUnknown`，则`ISetNextStatement`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[ISetNextStatement::CanSetNextStatement](../../winscript/reference/isetnextstatement-cansetnextstatement.md)|确定是否可以将执行点设置为指定的位置。|  
|[ISetNextStatement::SetNextStatement](../../winscript/reference/isetnextstatement-setnextstatement.md)|将执行点设置为指定的位置。|