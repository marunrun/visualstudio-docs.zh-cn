---
title: IEnumDebugPorts2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c30e42592af4d34765951b5e229555556c9b57b3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155022"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举的计算机或端口供应商提供的端口。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugPorts2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口来表示一系列由供应商创建的端口。 Visual Studio 实现此接口来支持其自己的端口提供程序。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)若要获取此界面表示创建的端口提供程序的端口的列表。 调用[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)获取表示已保存的端口的列表的此接口到磁盘。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugPorts2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|检索指定的数目的枚举序列中的端口。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|将跳过指定的数目的枚举序列中的端口。|  
|[Reset](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|获取一个枚举器中的端口数。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 将此接口来填充附加到进程所用端口的列表。  
  
 通常，调试引擎不使用此接口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)   
 [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)
