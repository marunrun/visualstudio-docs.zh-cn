---
title: IDebugPortSupplier3 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e4ece720cf6880bba528dee99cdbdeb25c10087a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674130"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口允许调用方确定端口提供程序是否可以调试器的调用之间保留 （通过将它们写入磁盘） 的端口，然后获取这些保留端口的列表。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPortSupplier3 : IDebugPortSupplier2  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口以支持持久保存或保存到磁盘的端口信息。 必须在与相同的对象上实现此接口[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上`IDebugPortSupplier2`接口，以获得此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了继承的方法之外[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)接口，此接口支持以下各项：  
  
|方法|描述|  
|------------|-----------------|  
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|返回是否端口提供程序可以保持不变的端口 （通过将它们写入磁盘） 的调试器调用之间。|  
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|返回可用于枚举通过已写入磁盘的此端口提供程序的所有端口的对象。|  
  
## <a name="remarks"></a>备注  
 如果端口提供程序可以在调用中保持原样的端口，它应实现此接口。 端口提供程序实例化，并且端口提供程序被销毁时写入磁盘时，应加载端口。  
  
 通常，调试引擎不与端口提供程序交互，并不会使用此接口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
