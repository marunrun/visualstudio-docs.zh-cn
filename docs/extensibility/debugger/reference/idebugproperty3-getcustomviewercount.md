---
title: IDebugProperty3::GetCustomViewerCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerCount
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerCount
ms.assetid: dc5bb3e4-dc85-46e4-98fa-c6be8583b985
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 99abfc65027bb43cafcd96c39da39ad40c5607ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348879"
---
# <a name="idebugproperty3getcustomviewercount"></a>IDebugProperty3::GetCustomViewerCount
获取自定义查看器可能适用于此属性的数目。

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
[out]自定义查看器可用于此属性的数目。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
为了支持类型可视化工具，此方法将调用转给[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)方法。 如果表达式计算器还支持用于此属性的类型的自定义查看器，此方法将自定义查看器数添加到返回的值。

有关类型可视化工具和自定义查看器之间的差异的详细信息，请参阅[类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CProperty**对象，它公开[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口。

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
