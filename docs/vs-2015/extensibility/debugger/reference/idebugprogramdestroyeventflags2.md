---
title: IDebugProgramDestroyEventFlags2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 86f7e211c742e4d95f3459d058139854874e7d85
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68182213"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]当您结束调试会话时，使调试引擎能够重写 UI 的默认行为。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgramDestroyEventFlags2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 此接口由调试引擎实现。 这适用于可能在进程的生存期内创建和销毁多个程序的主机。  
  
## <a name="methods"></a>方法  
 下表显示的方法 `IDebugProgramDestroyEventFlags2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|检索程序销毁标志。|  
  
## <a name="remarks"></a>备注  
 UI 的默认行为 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 是在所有程序都发送程序销毁事件后返回到设计模式。 此接口可使调试引擎更改该行为。  
  
## <a name="requirements"></a>要求  
 标头： Msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
