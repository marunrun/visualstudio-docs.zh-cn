---
title: IRemoteDebugApplication110 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication110 Interface
ms.assetid: 785ab46a-8827-41cb-806a-132e6b2c8f47
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea8f3f983cf7279cf6dc9600813a08268cef8301
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383498"
---
# <a name="iremotedebugapplication110-interface"></a>IRemoteDebugApplication110 接口
用于提供新功能，可调用脚本调试器和过程的调用方。  
  
> [!IMPORTANT]
> 此接口由 PDM v11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="methods"></a>方法  
 `IRemoteDebugApplication110` 接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IRemoteDebugApplication110::SetDebuggerOptions](../../winscript/reference/iremotedebugapplication110-setdebuggeroptions.md)|调用以更新调试器选项。 为 0 (SDO_NONE) 选项默认值。|  
|[IRemoteDebugApplication110::GetCurrentDebuggerOptions](../../winscript/reference/iremotedebugapplication110-getcurrentdebuggeroptions.md)|返回对当前已启用的选项集。|  
|[IRemoteDebugApplication110::GetMainThread](../../winscript/reference/iremotedebugapplication110-getmainthread.md)|返回主线程的调用 SetSite 的主机。|