---
title: IEnumCodePaths2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2
helpviewer_keywords:
- IEnumCodePaths2 interface
ms.assetid: 17ec9f9e-dc06-4532-b5db-da52efcc8630
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d5ad1f7a3f954116350e8accbdc9db02d0ac920d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319599"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
此接口表示的代码路径的列表。

## <a name="syntax"></a>语法

```
IEnumCodePaths2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口来表示一系列代码路径。

## <a name="notes-for-callers"></a>调用方的说明
 调用[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)若要获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IEnumCodePaths2`。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|检索指定的数目的枚举序列中的代码路径。|
|[Skip](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|将跳过指定的数目的枚举序列中的代码路径。|
|[Reset](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|将枚举序列重置到开头。|
|[Clone](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|获取一个枚举器中的代码路径的数量。|

## <a name="remarks"></a>备注
 代码路径表示在程序中的分支点或函数调用。 一系列代码路径表示的代码执行已通过其所采用的路径。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)