---
title: IDebug查询引擎2：：获取引擎接口 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2::GetEngineInterface
helpviewer_keywords:
- IDebugQueryEngine2::GetEngineInterface
ms.assetid: ed84aa98-7ec7-48f3-97ae-821090bc3664
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82f3214783a35e668bf3164c8659f60f863e9a43
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720663"
---
# <a name="idebugqueryengine2getengineinterface"></a>IDebugQueryEngine2::GetEngineInterface
获取自定义调试引擎 （DE） 接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineInterface( 
   IUnknown** ppUnk
);
```

```csharp
int GetEngineInterface( 
   out object ppUnk
);
```

## <a name="parameters"></a>参数
`ppUnk`\
[出]返回一`IUnknown`个对象表示调试引擎 （DE），该对象可以查询与 DE 关联的任何其他有效接口（例如[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)或[IDebugEngineLaunch2）。](../../../extensibility/debugger/reference/idebugenginelaunch2.md)

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 生成的接口应谨慎使用，因为通过此方法检索的接口调用会绕过会话调试管理器的处理，并可能导致 SDM 在调试时进入不良状态或生成错误。

## <a name="see-also"></a>请参阅
- [IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
