---
title: IEnumCodepath2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2
helpviewer_keywords:
- IEnumCodePaths2 interface
ms.assetid: 17ec9f9e-dc06-4532-b5db-da52efcc8630
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89c8cac9a7c2baa020002fe852330639d7081982
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717714"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
此接口表示代码路径的列表。

## <a name="syntax"></a>语法

```
IEnumCodePaths2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示代码路径的列表。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[EnumCodePath](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumCodePaths2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|检索枚举序列中指定数量的代码路径。|
|[跳](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|在枚举序列中跳过指定数量的代码路径。|
|[重置](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|获取枚举器中的代码路径数。|

## <a name="remarks"></a>备注
 代码路径表示程序中的分支点或函数调用。 代码路径列表表示代码执行所通过的路径。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
