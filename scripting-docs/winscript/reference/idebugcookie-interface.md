---
title: IDebugCookie 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugCookie interface
ms.assetid: 0dbc75d9-6f33-400f-a5bf-9122cf534082
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 47b48b917ee3376c417beffd9972d76a444513ef
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573191"
---
# <a name="idebugcookie-interface"></a>IDebugCookie 接口
允许设置调试 cookie，以与 `IMachineDebugManagerCookie` 接口一起使用。 有关详细信息，请参阅[IMachineDebugManagerCookie 接口](../../winscript/reference/imachinedebugmanagercookie-interface.md)。 此接口由进程调试管理器（PDM）实现并由脚本调试器使用。  
  
## <a name="methods"></a>方法  
 除了从 `IUnknown` 继承的方法之外，`IDebugCookie` 接口还公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugCookie::SetDebugCookie](../../winscript/reference/idebugcookie-setdebugcookie.md)|设置调试应用程序 cookie。|  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManagerCookie 接口](../../winscript/reference/imachinedebugmanagercookie-interface.md)