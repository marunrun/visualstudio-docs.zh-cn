---
title: IDebugPort供应商2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2
helpviewer_keywords:
- IDebugPortSupplier2 interface
ms.assetid: 37067324-2ea6-4a01-8829-a6e9c7a70068
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddce454e6634d8cc177019e9d30b0ffcc7e7f1cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724472"
---
# <a name="idebugportsupplier2"></a>IDebugPortSupplier2
此接口向会话调试管理器 （SDM） 提供端口。

## <a name="syntax"></a>语法

```
IDebugPortSupplier2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
自定义端口供应商实现此接口以表示端口供应商。

## <a name="notes-for-callers"></a>呼叫者备注
`CoCreateInstance`使用端口供应商的`GUID`调用返回此接口（这是获取此接口的典型方法）。 例如：

```cpp
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

对[GetPortSupplier 的](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)调用返回此接口，表示 正在使用的[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]当前端口供应商。

- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)返回此接口，表示创建端口的端口供应商。

- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)表示`IDebugPortSupplier`接口列表（`IEnumDebugPortSuppliers`接口是从[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)获取的，表示注册的所有[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]端口供应商）。

调试引擎通常不与端口供应商交互。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法`IDebugPortSupplier2`。

|方法|描述|
|------------|-----------------|
|[GetPortSupplierName](../../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)|获取端口供应商名称。|
|[GetPortSupplierId](../../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)|获取端口供应商标识符。|
|[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)|从端口供应商获取端口。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)|枚举已存在的端口。|
|[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)|验证端口供应商是否支持添加新端口。|
|[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)|添加端口。|
|[RemovePort](../../../extensibility/debugger/reference/idebugportsupplier2-removeport.md)|删除端口。|

## <a name="remarks"></a>备注
端口供应商可以按名称和 ID 标识自身，添加和删除端口，并枚举端口供应商提供的所有端口。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
