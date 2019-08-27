---
title: IDebugFirewallConfigurationCallback2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugFirewallConfigurationCallback2 interface
ms.assetid: 0827361c-b97c-4851-9898-ab6d88c81811
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 04d64ac489858e3a912b144b494430aec5b925d5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197053"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

允许使用 DCOM 提出的调试引擎[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]UI，以确保该防火墙将阻止远程调试。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugFirewallConfigurationCallback2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 会话调试管理器的端口对象由实现。  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDebugFirewallConfigurationCallback2`。  
  
|方法|描述|  
|------------|-----------------|  
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|该防火墙不阻止远程调试的请求。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
