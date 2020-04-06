---
title: IDebug 突破点决议2：：获取断点类型 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointResolution2::GetBreakpointType
helpviewer_keywords:
- IDebugBreakpointResolution2::GetBreakpointType
ms.assetid: 2b707fb9-f703-4c78-91bf-7434f57790a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2949366eeb3e79a732e94a4a8f8e9912048c6452
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734812"
---
# <a name="idebugbreakpointresolution2getbreakpointtype"></a>IDebugBreakpointResolution2::GetBreakpointType
获取此分辨率表示的断点的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBreakpointType( 
    BP_TYPE* pBPType
);
```

```csharp
int GetBreakpointType( 
    out enum_ BP_TYPE pBPType
);
```

## <a name="parameters"></a>参数
`pBPType`\
[出]从[BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)枚举中返回指定此断点类型的值。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则返回错误代码。 如果关联的BP_RESOLUTION_INFO结构`bpResLocation`中的字段无效，[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)则返回E_FAIL。

## <a name="remarks"></a>备注
例如，断点可以是代码或数据断点。

## <a name="example"></a>示例
下面的示例演示如何为公开`CDebugBreakpointResolution`[IDebugBreakpointE2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)接口的简单对象实现此方法。

```
HRESULT CDebugBreakpointResolution::GetBreakpointType(BP_TYPE* pBPType)
{
    HRESULT hr;

    if (pBPType)
    {
        // Set default BP_TYPE.
        *pBPType = BPT_NONE;

        // Check if the BPRESI_BPRESLOCATION flag is set in BPRESI_FIELDS.
        if (IsFlagSet(m_bpResolutionInfo.dwFields, BPRESI_BPRESLOCATION))
        {
            // Set the new BP_TYPE.
            *pBPType = m_bpResolutionInfo.bpResLocation.bpType;
            hr = S_OK;
        }
        else
        {
            hr = E_FAIL;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
