---
title: IDebugPortSupplier2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2
helpviewer_keywords:
- IDebugPortSupplier2 interface
ms.assetid: 37067324-2ea6-4a01-8829-a6e9c7a70068
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b6d9c3f8b45affd192d4109db08454345dcd0814
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188221"
---
# <a name="idebugportsupplier2"></a>IDebugPortSupplier2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口提供了会话调试管理器 (SDM) 的端口。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPortSupplier2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口来表示端口提供程序。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用`CoCreateInstance`与端口供应商的`GUID`返回 （这是典型的方法来获取此接口） 此接口。 例如：  
  
```cpp#  
IDebugPortSupplier2 *GetPortSupplier(GUID *pPortSupplierGuid)  
{  
    IDebugPortSupplier2 *pPS = NULL;  
    if (pPortSupplierGuid != NULL) {  
        CComPtr<IDebugPortSupplier2> spPortSupplier;  
        spPortSupplier.CoCreateInstance(*pPortSupplierGuid);  
        if (spPortSupplier != NULL) {  
            pPS = spPortSupplier.Detach();  
        }  
    }  
    return (pPS);  
}  
```  
  
 调用[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)返回此接口，表示当前正在使用的端口提供程序[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]。  
  
 [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)返回此接口，它表示创建此端口的端口提供程序。  
  
 [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)表示一系列`IDebugPortSupplier`接口 (`IEnumDebugPortSuppliers`接口的均来自[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)，表示所有端口提供程序都注册到[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]).  
  
 调试引擎通常不与端口提供程序交互。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugPortSupplier2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetPortSupplierName](../../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)|获取端口供应商名称。|  
|[GetPortSupplierId](../../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)|获取端口供应商标识符。|  
|[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)|获取一个端口从端口提供程序。|  
|[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)|枚举已存在的端口。|  
|[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)|验证端口提供程序支持添加新端口。|  
|[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)|将添加一个端口。|  
|[RemovePort](../../../extensibility/debugger/reference/idebugportsupplier2-removeport.md)|删除端口。|  
  
## <a name="remarks"></a>备注  
 端口提供程序可以按名称和 ID 将自身标识、 添加和删除的端口，以及枚举端口供应商提供的所有端口。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)   
 [GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)   
 [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
