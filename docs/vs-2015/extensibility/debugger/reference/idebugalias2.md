---
title: IDebugAlias2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugAlias2 interface
ms.assetid: 5252dcbb-8bfe-4d8a-a8e5-b022b194df19
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 951f0dde4dbd57ac18269adedd77c8f6d7ccdd5e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63410095"
---
# <a name="idebugalias2"></a>IDebugAlias2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示的数值别名的变量，并可将表达式计算器 (EE) 来获取该别名的应用程序域。

## <a name="syntax"></a>语法

```
IDebugAlias2 : IDebugAlias
```

## <a name="notes-for-implementers"></a>实施者的说明
 托管的调试引擎 (DE) 实现此接口。

## <a name="methods"></a>方法
 除了上的方法[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)接口，此接口实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetAppDomainId](../../../extensibility/debugger/reference/idebugalias2-getappdomainid.md)|检索应用程序域标识符。|

## <a name="remarks"></a>备注
 别名是以字符串形式的 # 字符，例如 1001 # 后跟一个十进制数。

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll