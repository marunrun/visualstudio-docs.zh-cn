---
title: IDebugAlias2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugAlias2 interface
ms.assetid: 5252dcbb-8bfe-4d8a-a8e5-b022b194df19
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00e13da257c5477b3834ebb85bf6d481fe699362
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736364"
---
# <a name="idebugalias2"></a>IDebugAlias2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示变量的数字别名，并使表达式赋值器 （EE） 能够获取别名的应用程序域。

## <a name="syntax"></a>语法

```
IDebugAlias2 : IDebugAlias
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由托管调试引擎 （DE） 实现。

## <a name="methods"></a>方法
 除了[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetAppDomainId](../../../extensibility/debugger/reference/idebugalias2-getappdomainid.md)|检索应用程序域的标识符。|

## <a name="remarks"></a>备注
 别名是字符串形式的十进制数字，后跟 # 字符，例如 1001*。

## <a name="requirements"></a>要求
 标题： Ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
