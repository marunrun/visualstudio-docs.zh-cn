---
title: IDebugModOpt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d9f8fa5e496056eac2a30114f4062f635775350b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324055"
---
# <a name="idebugmodopt"></a>IDebugModOpt
表示调试可选修饰符。

## <a name="syntax"></a>语法

```
IDebugModOpt : IUnknown
```

## <a name="notes-for-callers"></a>调用方的说明
 从获取[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)表示类或方法的对象。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|检索一组可选的修饰符。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll