---
title: IDebugThreadCall 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugThreadCall interface
ms.assetid: 9a9a9892-f310-4ef3-8db2-4f868be52d7e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 89f0fba2f5210cdcf4bb8f17443f948cb9ba1f4e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004854"
---
# <a name="idebugthreadcall-interface"></a>IDebugThreadCall 接口
`IDebugThreadCall`界面通常由组件可以使用的跨线程调用实现`IDebugThread`封送由进程调试管理器 (PDM) 提供实现。  
  
 PDM 调用`IDebugThreadCall`中所需的线程，接口和`IDebugThreadCall`接口将调度到所需的实现调用。 `IDebugThreadCall`接口将强制转换到适当的顶部的参数中传递的参数信息。  
  
 `IDebugThreadCall`接口是自由线程对象。  
  
## <a name="methods"></a>方法  
 除了继承的方法之外`IUnknown`，则`IDebugThreadCall`接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugThreadCall::ThreadCallHandler](../../winscript/reference/idebugthreadcall-threadcallhandler.md)|处理调用另一线程中运行代码。|