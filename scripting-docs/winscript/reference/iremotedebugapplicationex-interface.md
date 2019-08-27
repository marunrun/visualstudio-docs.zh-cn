---
title: IRemoteDebugApplicationEx 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplicationEx Interface
ms.assetid: 8e16164d-dbb2-4488-9507-25ae34f343dc
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ab9e25a28ade1ac73b9e4837dae61e2d91f24c45
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788373"
---
# <a name="iremotedebugapplicationex-interface"></a>IRemoteDebugApplicationEx 接口
表示正在运行的应用程序。 它不需要以与操作系统进程相对应。 通常情况下，调试器以用于调试的应用程序目标。 进程调试管理器通常实现应用程序对象。  
  
 除了继承的方法之外`IUnknown`，则`IRemoteDebugApplicationEx`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IRemoteDebugApplicationEx:GetHostPid](../../winscript/reference/iremotedebugapplicationex-gethostpid.md)|返回主机应用程序的进程 ID。|  
|GetHostMachineName|返回的计算机上运行主机应用程序的名称。|  
|[IRemoteDebugApplicationEx:SetLocale](../../winscript/reference/iremotedebugapplicationex-setlocale.md)|设置调试器本地化的语言。|  
|[IRemoteDebugApplicationEx:ForceStepMode](../../winscript/reference/iremotedebugapplicationex-forcestepmode.md)|强制调试器单步执行模式。|  
|[IRemoteDebugApplicationEx:RevokeBreak](../../winscript/reference/iremotedebugapplicationex-revokebreak.md)|撤消换行命令。|  
|SetProxyBlanketAndAddRef|更新对调试器对象的代理，以确保与从基于 Windows 95 的操作系统进行远程调试的兼容性的 COM 安全信息。|  
|ReleaseFromSetProxyBlanket|从 SetProxyBlanketAndAddRef 版本 AddRef。|