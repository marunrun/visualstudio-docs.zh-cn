---
title: IDebug属性3：：获取自定义查看器计数 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerCount
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerCount
ms.assetid: dc5bb3e4-dc85-46e4-98fa-c6be8583b985
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 16cb623f58668362e5e308e1d66dfd6ca7c0fb8c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721195"
---
# <a name="idebugproperty3getcustomviewercount"></a>IDebugProperty3::GetCustomViewerCount
获取可能可用于此属性的自定义查看器数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomViewerCount(
    ULONG* pcelt
);
```

```csharp
int GetCustomViewerCount(
    out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
[出]可用于此属性的自定义查看器数。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
为了支持类型可视化工具，此方法将调用转发到[GetCustomViewerCount 方法](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)。 如果表达式赋值器还支持此属性类型的自定义查看器，则此方法会将自定义查看器的数量添加到返回的值。

有关类型可视化器和自定义查看器之间的差异的详细信息，请参阅[类型可视化器和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口的**CProperty**对象实现此方法。

```cpp
STDMETHODIMP CProperty::GetCustomViewerCount(ULONG* pcelt)
{
    if (pcelt == NULL)
    {
        return E_POINTER;
    }

    if (GetVisualizerService())
    {
        return m_pIEEVisualizerService->GetCustomViewerCount(pcelt);
    }
    else
    {
        return E_NOTIMPL;
    }
}
```

## <a name="see-also"></a>请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
