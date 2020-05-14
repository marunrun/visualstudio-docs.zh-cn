---
title: IDebugCodeContext3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e3f81168d9af7fbbb93b5c59f3ab19a17107b56b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734184"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
扩展[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)接口，以便检索模块和进程接口。

## <a name="syntax"></a>语法

```
IDebugCodeContext3 : IDebugCodeContext2
```

## <a name="notes-for-implementers"></a>实施者说明
 由调试引擎实现，并由[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试包使用。

## <a name="methods"></a>方法
 除了接口上的方法外`IDebugCodeContext2`，此接口还实现以下方法：

|方法|描述|
|------------|-----------------|
|[获取模块](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|检索对调试模块接口的引用。|
|[获取过程](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|检索对调试过程接口的引用。|

## <a name="remarks"></a>备注
 这是一个可选的接口，通常不需要实现。

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
