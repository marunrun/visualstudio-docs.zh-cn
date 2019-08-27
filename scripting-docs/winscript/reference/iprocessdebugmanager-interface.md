---
title: IProcessDebugManager Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IProcessDebugManager interface
ms.assetid: b6ecb2bd-a4d1-4857-9232-036c154d0cb1
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d68c044cdc3d523841cc56814b8ca34bcd8aa037
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62944792"
---
# <a name="iprocessdebugmanager-interface"></a>IProcessDebugManager 接口
进程调试管理器的主接口。 此接口可以在进程中创建、添加或删除虚拟应用程序。 它可以枚举堆栈帧和应用程序线程。  
  
 除了继承的方法之外`IUnknown`，则`IProcessDebugManager`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IProcessDebugManager::CreateApplication](../../winscript/reference/iprocessdebugmanager-createapplication.md)|创建一个新的调试应用程序对象，此应用程序。|  
|[IProcessDebugManager::GetDefaultApplication](../../winscript/reference/iprocessdebugmanager-getdefaultapplication.md)|返回当前进程的默认应用程序对象。|  
|[IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)|将添加到计算机调试管理器的列表正在运行的应用程序的应用程序。|  
|[IProcessDebugManager::RemoveApplication](../../winscript/reference/iprocessdebugmanager-removeapplication.md)|删除应用程序从正在运行的应用程序列表。|  
|[IProcessDebugManager::CreateDebugDocumentHelper](../../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md)|创建此应用程序的新调试文档帮助程序。|