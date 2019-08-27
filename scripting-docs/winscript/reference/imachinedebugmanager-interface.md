---
title: IMachineDebugManager 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManager interface
ms.assetid: 0b7133bb-5a52-4036-b4db-d69260790db7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6db8989fc6c932723a9b95017854635396b0deda
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977638"
---
# <a name="imachinedebugmanager-interface"></a>IMachineDebugManager 接口
计算机调试管理器主接口。 此接口是类似于`IMachineDebugManagerCookie`接口。  
  
 除了继承的方法之外`IUnknown`，则`IMachineDebugManager`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IMachineDebugManager::AddApplication](../../winscript/reference/imachinedebugmanager-addapplication.md)|将添加到正在运行的应用程序的应用程序列表。|  
|[IMachineDebugManager::RemoveApplication](../../winscript/reference/imachinedebugmanager-removeapplication.md)|删除应用程序从正在运行的应用程序列表。|  
|[IMachineDebugManager::EnumApplications](../../winscript/reference/imachinedebugmanager-enumapplications.md)|返回当前正在运行的应用程序的列表的枚举器。|  
  
## <a name="see-also"></a>请参阅  
 [IMachineDebugManagerCookie 接口](../../winscript/reference/imachinedebugmanagercookie-interface.md)