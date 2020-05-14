---
title: IDebug动态场+ |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus interface
ms.assetid: c3a25f27-327a-4bdb-b026-27d436ddcd0c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 823057303655da59494680ce9f591b252e28f792
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731224"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
表示[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象的动态字段。

## <a name="syntax"></a>语法

```
IDebugDynamicFieldCOMPlus : IDebugDynamicField
```

## <a name="methods"></a>方法
 除了[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|检索给定其基元类型的类型。|
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|检索给定其令牌的类型。|

## <a name="requirements"></a>要求
 标题： Sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
