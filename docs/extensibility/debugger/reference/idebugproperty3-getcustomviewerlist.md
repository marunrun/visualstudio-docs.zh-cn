---
title: IDebugProperty3::GetCustomViewerList |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerList
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerList
ms.assetid: 74490fd8-6f44-4618-beea-dab64961bb8a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5d8a439863f577237699950b3d70eb15d75ec77a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348873"
---
# <a name="idebugproperty3getcustomviewerlist"></a>IDebugProperty3::GetCustomViewerList
获取与此属性关联的自定义查看器的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomViewerList(
    ULONG                celtSkip,
    ULONG                celtRequested,
    DEBUG_CUSTOM_VIEWER* rgViewers,
    ULONG*               pceltFetched
);
```

```csharp
int GetCustomViewerList(
    uint                  celtSkip,
    uint                  celtRequested,
    DEBUG_CUSTOM_VIEWER[] rgViewers,
    out uint              pceltFetched
);
```

## <a name="parameters"></a>参数
`celtSkip`\
[in]若要跳过的查看者数。

`celtRequested`\
[in]若要检索的查看者数 (还指定的大小`rgViewers`数组)。

`rgViewers`\
[in、 out]数组[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)要填充的结构。

`pceltFetched`\
[out]返回的查看器的实际数目。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
若要支持类型可视化工具，此方法将调用转发到[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)方法。 如果表达式计算器还支持用于此属性的类型的自定义查看器，此方法可以将相应自定义查看器附加到列表。

请参阅[类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)有关类型可视化工具和自定义查看器之间的差异的详细信息。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CProperty**对象，它公开[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口。

```cpp
STDMETHODIMP CProperty::GetCustomViewerList(ULONG celtSkip, ULONG celtRequested, DEBUG_CUSTOM_VIEWER* prgViewers, ULONG* pceltFetched)
{
    if (NULL == prgViewers)
    {
        return E_POINTER;
    }

    if (GetVisualizerService())
    {
        return m_pIEEVisualizerService->GetCustomViewerList(celtSkip, celtRequested, prgViewers, pceltFetched);
    }
    else
    {
        return E_NOTIMPL;
    }
}
```

## <a name="see-also"></a>请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
