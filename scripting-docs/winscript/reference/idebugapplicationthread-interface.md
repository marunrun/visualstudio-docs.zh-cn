---
title: IDebugApplicationThread 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThread interface
ms.assetid: f869c328-4409-4b74-a6c3-9e63fc58c63d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a464085eddbea4f5d29c684c0f1dabc6f853b6d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822221"
---
# <a name="idebugapplicationthread-interface"></a>IDebugApplicationThread 接口
允许语言引擎和主机提供线程同步和维护特定于线程的调试状态信息。 此接口扩展`IRemoteDebugApplicationThread`接口，以提供非远程访问该线程。  
  
 除了继承的方法之外`IRemoteDebugApplicationThread`，则`IDebugApplicationThread`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugApplicationThread::SynchronousCallIntoThread](../../winscript/reference/idebugapplicationthread-synchronouscallintothread.md)|提供了为使调用方应用程序线程中运行代码的机制。|  
|[IDebugApplicationThread::QueryIsCurrentThread](../../winscript/reference/idebugapplicationthread-queryiscurrentthread.md)|确定此线程是否当前正在运行的线程。|  
|[IDebugApplicationThread::QueryIsDebuggerThread](../../winscript/reference/idebugapplicationthread-queryisdebuggerthread.md)|确定此线程是调试器线程。|  
|[IDebugApplicationThread::SetDescription](../../winscript/reference/idebugapplicationthread-setdescription.md)|设置此线程的说明。|  
|[IDebugApplicationThread::SetStateString](../../winscript/reference/idebugapplicationthread-setstatestring.md)|设置线程状态的说明。|