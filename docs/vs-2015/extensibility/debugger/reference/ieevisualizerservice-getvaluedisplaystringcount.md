---
title: IEEVisualizerService::GetValueDisplayStringCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IEEVisualizerService::GetValueDisplayStringCount
- GetValueDisplayStringCount
ms.assetid: d683a833-fbfb-4042-84df-6905124a268a
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6785be367430443f92a9cc54a2d636582053228e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192094"
---
# <a name="ieevisualizerservicegetvaluedisplaystringcount"></a>IEEVisualizerService::GetValueDisplayStringCount
检索要显示为指定的属性或字段的值字符串数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetValueDisplayStringCount (
   DWORD         displayKind,
   IDebugField * propertyOrField,
   ULONG *       pcelt
);
```

```csharp
int GetValueDisplayStringCount (
   uint        displayKind,
   IDebugField propertyOrField,
   out ulong   pcelt
);
```

#### <a name="parameters"></a>参数
 `displayKind`

 [in]值从[DisplayKind](../../../extensibility/debugger/reference/displaykind.md)枚举。

 `propertyOrField`

 [in][IDebugField](../../../extensibility/debugger/reference/idebugfield.md)表示属性或字段的接口。

 `pcelt`

 [out]返回要显示的值字符串数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)