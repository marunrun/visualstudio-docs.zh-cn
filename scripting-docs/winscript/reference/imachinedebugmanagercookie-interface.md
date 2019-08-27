---
title: IMachineDebugManagerCookie Interface | Microsoft Docs
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
ms.openlocfilehash: fdc02498360f2e3900012166474c5d1e35abd6ee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977677"
---
# <a name="imachinedebugmanagercookie-interface"></a>IMachineDebugManagerCookie 接口
类似于`IMachineDebugManager`接口，`IMachineDebugManagerCookie`接口支持调试 cookie。  
  
 此接口 (连同`IDebugCookie`接口) 允许脚本在脚本调试器进程中运行而无需调试器保持跟踪的这些脚本。  
  
 脚本调试程序调用`IDebugCookie::SetDebugCookie`方法进程调试管理器 (PDM)。 然后，PDM 发送了此 cookie 和添加或删除脚本的应用程序到或从计算机调试管理器 (MDM)，任何请求一起使用的方法`IMachineDebugManagerCookie`接口。 MDM 然后通知每个更改，除具有该 cookie 的调试器。  
  
 除了继承的方法之外`IUnknown`，则`IMachineDebugManagerCookie`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IMachineDebugManagerCookie::AddApplication](../../winscript/reference/imachinedebugmanagercookie-addapplication.md)|将添加到正在运行的应用程序的应用程序列表。|  
|[IMachineDebugManagerCookie::EnumApplications](../../winscript/reference/imachinedebugmanagercookie-enumapplications.md)|返回当前正在运行的应用程序的列表的枚举器。|  
|[IMachineDebugManagerCookie::RemoveApplication](../../winscript/reference/imachinedebugmanagercookie-removeapplication.md)|删除应用程序从正在运行的应用程序列表。|  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManager 接口](../../winscript/reference/imachinedebugmanager-interface.md)   
 [IDebugCookie 接口](../../winscript/reference/idebugcookie-interface.md)