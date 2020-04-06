---
title: IEnumDebugCode_s______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6917c44bb3ddc80513e7c45a6aa4ea0207fd46c9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717279"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
此接口枚举与调试会话或特定程序或文档关联的代码上下文。

## <a name="syntax"></a>语法

```
IEnumDebugCodeContexts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示程序中特定文本位置的代码上下文列表或特定文档上下文的代码上下文列表。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[EnumCodeContext](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)以获取此接口，该接口表示程序源文档中特定文本位置的代码上下文列表。

 调用[EnumCodeContext](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)以获取此接口，以表示特定源文档中所有代码上下文的列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugCodeContexts2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|检索枚举序列中指定数量的代码上下文。|
|[跳](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|在枚举序列中跳过指定数量的代码上下文。|
|[重置](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|获取枚举器中的代码上下文数。|

## <a name="remarks"></a>备注
 Visual Studio 调用[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)来填充用户在设置下一个语句或显示源文件的拆解时可以选择的代码上下文列表。 例如，当C++模板有多个实例时，可能会发生多个代码上下文。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)
