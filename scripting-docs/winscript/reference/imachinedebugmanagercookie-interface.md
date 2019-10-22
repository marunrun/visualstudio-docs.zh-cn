---
title: IMachineDebugManagerCookie 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManagerCookie interface
ms.assetid: 04770935-3ccf-41e9-b0c1-c78376ab1e3c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b39c286f389c99187b0f3250fc68af92ff5dcc8
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573888"
---
# <a name="imachinedebugmanagercookie-interface"></a>IMachineDebugManagerCookie 接口
与 `IMachineDebugManager` 接口类似，`IMachineDebugManagerCookie` 接口支持调试 cookie。  
  
 此接口（连同 `IDebugCookie` 接口）允许脚本在脚本调试器进程中运行，而无需调试器跟踪这些脚本。  
  
 脚本调试器在进程调试管理器（PDM）上调用 `IDebugCookie::SetDebugCookie` 方法。 然后，PDM 将与任何请求一起发送此 cookie，以便使用 `IMachineDebugManagerCookie` 接口的方法向/从计算机调试管理器（MDM）添加或删除脚本应用程序。 然后，MDM 将通知每个更改，其中包含该 cookie 的每个调试器除外。  
  
 除了从 `IUnknown` 继承的方法之外，`IMachineDebugManagerCookie` 接口还公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IMachineDebugManagerCookie::AddApplication](../../winscript/reference/imachinedebugmanagercookie-addapplication.md)|将应用程序添加到正在运行的应用程序列表中。|  
|[IMachineDebugManagerCookie::EnumApplications](../../winscript/reference/imachinedebugmanagercookie-enumapplications.md)|返回当前正在运行的应用程序列表的枚举器。|  
|[IMachineDebugManagerCookie::RemoveApplication](../../winscript/reference/imachinedebugmanagercookie-removeapplication.md)|从正在运行的应用程序列表中删除应用程序。|  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManager 接口](../../winscript/reference/imachinedebugmanager-interface.md)   
 [IDebugCookie 接口](../../winscript/reference/idebugcookie-interface.md)