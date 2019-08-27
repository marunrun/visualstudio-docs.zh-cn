---
title: IDebugBreakpointRequest3::GetRequestInfo2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3::GetRequestInfo2
helpviewer_keywords:
- IDebugBreakpointRequest3::GetRequestInfo2
ms.assetid: 33942e4a-0a0a-49e8-a693-004954f6d38a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86e687a02e434c12c6386df57462cdb578250cdd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324212"
---
# <a name="idebugbreakpointrequest3getrequestinfo2"></a>IDebugBreakpointRequest3::GetRequestInfo2
此方法获取描述此断点请求的断点请求信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetRequestInfo2(
   BPREQI_FIELDS      dwFields,
   BP_REQUEST_INFO2*  bBPRequestInfo
);
```

```csharp
int GetRequestInfo2(
   enum_BPREQI_FIELDS  dwFields,
   BP_REQUEST_INFO2[]  bBPRequestInfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]中的标志的组合[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举，用于确定哪些字段的`pBPRequestInfo`要填充的。

`bBPRequestInfo`\
[out][BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)要填充的结构。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="remarks"></a>备注
 在此请求中不是从返回的详细信息[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)