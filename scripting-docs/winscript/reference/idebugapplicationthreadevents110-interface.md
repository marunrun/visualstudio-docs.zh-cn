---
title: IDebugApplicationThreadEvents110 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationThreadEvents110 Interface
ms.assetid: 91a98b0e-7c81-4118-af75-82f75fd4f25a
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b2cdde46484f95aa57404ebe6b6cb4c86ef458c9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440504"
---
# <a name="idebugapplicationthreadevents110-interface"></a>IDebugApplicationThreadEvents110 接口
将添加更多的线程事件。 这些事件仅是本地的。 也就是说，您可以订阅它们仅在进程正在调试，请使用[IConnectionPoint](http://go.microsoft.com/fwlink/?LinkId=232738)通知和取消方法通知 PDM 应用程序线程对象 (对象实现[IDebugApplicationThread接口](../../winscript/reference/idebugapplicationthread-interface.md))。 从新提供的线程上发生。  
  
> [!IMPORTANT]
> 此接口由 PDM v11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="methods"></a>方法  
 `IDebugActivationThreadEvents110` 接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugApplicationThreadEvents110 ::OnBeginThreadRequest](../../winscript/reference/idebugapplicationthreadevents110-onbeginthreadrequest.md)|调用到使用 PDM 的线程的线程切换已开始。|  
|[IDebugApplicationThreadEvents110::OnResumeFromBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onresumefrombreakpoint.md)|该线程从断点恢复，并将再一次处于活动状态。|  
|[IDebugApplicationThreadEvents110::OnSuspendForBreakPoint](../../winscript/reference/idebugapplicationthreadevents110-onsuspendforbreakpoint.md)|线程正在挂起断点，可以处理需要完全挂起的线程的调用。|  
|[IDebugApplicationThreadEvents110::OnThreadRequestComplete](../../winscript/reference/idebugapplicationthreadevents110-onthreadrequestcomplete.md)|调用到使用 PDM 的线程的线程切换已完成。|