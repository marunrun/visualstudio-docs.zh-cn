---
title: IEnumDebugProcesses2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2
helpviewer_keywords:
- IEnumDebugProcesses2
ms.assetid: 06a1368f-10f0-44eb-af61-e388c2327111
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d56d284d08a1c6b55318300ef7e1db1e385d584e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178426"
---
# <a name="ienumdebugprocesses2"></a>IEnumDebugProcesses2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举调试端口上运行的进程。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugProcesses : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口可提供一个端口上运行的进程的列表。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 Visual Studio 调用[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)若要获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugProcesses2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)|检索指定的数目的枚举序列中的进程。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugprocesses2-skip.md)|跳过枚举序列中的进程的指定的数目。|  
|[Reset](../../../extensibility/debugger/reference/ienumdebugprocesses2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugprocesses2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprocesses2-getcount.md)|获取一个枚举器中的进程数。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 使用此接口来填充**进程**窗口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)
