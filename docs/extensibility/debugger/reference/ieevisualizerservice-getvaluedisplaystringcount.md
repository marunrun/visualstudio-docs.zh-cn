---
title: IEEVisualizerService::GetValueDisplayStringCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IEEVisualizerService::GetValueDisplayStringCount
- GetValueDisplayStringCount
ms.assetid: d683a833-fbfb-4042-84df-6905124a268a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20e09dad1d87df646d1dc8ef7509842b49a8cdaa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308923"
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

## <a name="parameters"></a>参数
`displayKind`\
[in]值从[DisplayKind](../../../extensibility/debugger/reference/displaykind.md)枚举。

`propertyOrField`\
[in][IDebugField](../../../extensibility/debugger/reference/idebugfield.md)表示属性或字段的接口。

`pcelt`\
[out]返回要显示的值字符串数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)