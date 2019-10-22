---
title: Windows 脚本宿主 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows Script Host, implementing hosts
ms.assetid: 9d5f6471-b318-40f3-be01-d9cd0b1cdd47
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8468f578ee44487acd2575e81e01d65969110437
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72568810"
---
# <a name="windows-script-hosts"></a>Windows 脚本宿主
实现 Microsoft Windows 脚本宿主时，只要宿主执行以下操作，即可以大胆地假定脚本引擎只在基础线程的上下文中调用 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 接口：  
  
- 选择基础线程（通常是包含消息循环的线程）。  
  
- 在基础线程中实例化脚本引擎。  
  
- 只从基础线程调用脚本引擎方法，经过明确允许时除外（例如在使用 [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) 和 [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) 时）。  
  
- 只从基础线程调用脚本引擎的调度对象。  
  
- 提供窗口句柄后确保消息循环在基础线程中运行。  
  
- 确保宿主的对象模型中的对象只获取基础线程中的事件。  
  
  所有的单一线程宿主均自动遵守这些规则。 将上述受限制的模型有意设计得较为松散，以允许宿主可以从其他线程调用 [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md)（通过 CTRL+BREAK 处理程序或类似程序启动）来中止卡滞的脚本，或允许宿主使用 [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) 复制新线程中的脚本。  
  
## <a name="remarks"></a>备注  
 这些限制均不适用于选择实现自由线程 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 接口和自由线程对象模型的宿主。 此类宿主可以使用任意线程中的 [IActiveScript](../winscript/reference/iactivescript.md) 接口，而不受任何限制。  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口](../winscript/windows-script-interfaces.md)