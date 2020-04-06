---
title: IDebugEngine2：：获取引擎ID |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::GetEngineID
helpviewer_keywords:
- IDebugEngine2::GetEngineID
ms.assetid: 0d5674c8-a9b9-4b72-8211-d2d68695775a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f4071e8279c2c4ab615ff625c1bbedebfd8e64ad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731077"
---
# <a name="idebugengine2getengineid"></a>IDebugEngine2::GetEngineID
获取调试引擎 （DE） 的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineID(
    GUID* pguidEngine
);
```

```csharp
int GetEngineID(
    out Guid pguidEngine
);
```

## <a name="parameters"></a>参数
`pguidEngine`\
[出]返回 DE 的 GUID。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
典型 GUID 的一些`guidScriptEng`示例`guidNativeEng`是`guidSQLEng`， 或 。 新的调试引擎将创建自己的 GUID 进行标识。

## <a name="example"></a>示例
下面的示例演示如何实现[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口的简单`CEngine`对象实现此方法。

```cpp
HRESULT CEngine::GetEngineId(GUID *pguidEngine) {
    if (pguidEngine) {
        // Set pguidEngine to guidBatEng, as defined in the Batdbg.idl file.
        // Other languages would require their own guidDifferentEngine to be
        //defined in the Batdbg.idl file.
        *pguidEngine = guidBatEng;
        return NOERROR; // This is typically S_OK.
    } else {
        return E_INVALIDARG;
    }
}
```

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
