---
title: IDebugFirewallConfigurationCallback2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197053"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

启用使用 DCOM 来要求 UI 的调试引擎， [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 以确保防火墙不会阻止远程调试。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugFirewallConfigurationCallback2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 由会话调试管理器的端口对象实现。  
  
## <a name="methods"></a>方法  
 下表显示的方法 `IDebugFirewallConfigurationCallback2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|请求防火墙不阻止远程调试。|  
  
## <a name="requirements"></a>要求  
 标头： Msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
