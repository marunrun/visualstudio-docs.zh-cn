---
title: IDebug函数对象2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c4150480d2e6686992d78727b6fed817da270145
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728426"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示函数并增强[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。

## <a name="syntax"></a>语法

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器 （EE） 实现此接口以表示函数。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口的方法以下列方式递延**IDebug函数对象**的方法：

- **IDebug评估**方法采用标志。

- **CreateObject**方法采用标志和超时。

- **使用长度创建 StringObject**方法需要一段长度。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|创建使用构造函数给定评估标志设置和超时值的对象。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|创建具有指定长度的字符串对象。|
|[评估](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|调用函数并将结果值作为对象返回。|

## <a name="requirements"></a>要求
 标题： Ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
