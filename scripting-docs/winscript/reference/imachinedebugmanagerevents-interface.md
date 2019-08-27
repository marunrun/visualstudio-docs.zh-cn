---
title: IMachineDebugManagerEvents Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManagerEvents interface
ms.assetid: 468de2f4-49e0-4f6f-ba0c-0f5f6832c092
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fcfcc2aed0fedefdc149b83e911d33cd3b54cdef
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977625"
---
# <a name="imachinedebugmanagerevents-interface"></a>IMachineDebugManagerEvents 接口
由计算机调试管理器维护的正在运行的应用程序列表中的信号变化。 此接口可以由调试器 IDE，用于显示应用程序的动态列表。  
  
 除了继承的方法之外`IUnknown`，则`IMachineDebugManagerEvents`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IMachineDebugManagerEvents::onAddApplication](../../winscript/reference/imachinedebugmanagerevents-onaddapplication.md)|处理事件时应用程序添加到正在运行的应用程序列表。|  
|[IMachineDebugManagerEvents::onRemoveApplication](../../winscript/reference/imachinedebugmanagerevents-onremoveapplication.md)|处理事件时应用程序删除从正在运行的应用程序列表。|