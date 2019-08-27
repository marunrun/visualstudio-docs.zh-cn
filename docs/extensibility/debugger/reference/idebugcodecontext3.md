---
title: IDebugCodeContext3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db3b27e510ccdbb5ec55c5bfae373114df0c9b16
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338972"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
扩展了[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)接口以便可以检索模块并处理的接口。

## <a name="syntax"></a>语法

```
IDebugCodeContext3 : IDebugCodeContext2
```

## <a name="notes-for-implementers"></a>实施者的说明
 由的调试引擎实现并由[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]调试包。

## <a name="methods"></a>方法
 除了上的方法`IDebugCodeContext2`接口，此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|检索到的调试模块接口的引用。|
|[GetProcess](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|检索到的调试进程的接口的引用。|

## <a name="remarks"></a>备注
 这是通常不需要实现的可选接口。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll