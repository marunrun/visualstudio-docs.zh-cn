---
title: IDebugProgramHost2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2bcb65872f9f451e1cc4e5030532e0a444af1139
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687785"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供有关程序的主机 （进程） 信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgramHost2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎与相同的对象上实现此接口[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口，以提供有关托管进程的信息。 这是可选的接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上`IDebugProgram2`接口，以获得此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugProgramHost2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|获取标题、 友好名称或此程序的宿主进程的文件名。|  
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|获取此程序的宿主进程的进程标识符。|  
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|获取此程序的宿主进程运行的计算机的名称。|  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
