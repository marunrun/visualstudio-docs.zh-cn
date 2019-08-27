---
title: IDebugIDECallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback interface
ms.assetid: 8d31adc0-1c44-4658-8d4f-f4b73e35f4a6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d5a489256b14b828fd548b3e2da3c2c02f9d5317
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349569"
---
# <a name="idebugidecallback"></a>IDebugIDECallback
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 启用要在调试器的输出窗口中显示一条消息的表达式计算器 (EE)。

## <a name="syntax"></a>语法

```
IDebugIDECallback : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 托管的调试引擎实现此回调。

## <a name="notes-for-callers"></a>调用方的说明
 它可供的表达式计算器将输出发送到调试器的输出窗口。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[DisplayMessage](../../../extensibility/debugger/reference/idebugidecallback-displaymessage.md)|将指定的消息字符串发送到调试器的输出窗口。|

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll