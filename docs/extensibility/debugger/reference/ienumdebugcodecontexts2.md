---
title: IEnumDebugCodeContexts2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dae1261adca25162b5bb81cc3ae8b006ce7ef283
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350878"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
此接口枚举与调试会话，或与特定的程序或文档关联的代码上下文。

## <a name="syntax"></a>语法

```
IEnumDebugCodeContexts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口来表示在程序中，特定的文本位置的代码上下文的列表或特定文档上下文的代码上下文的列表。

## <a name="notes-for-callers"></a>调用方的说明
 调用[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)若要获取此界面表示程序的源文档中的特定文本位置的代码上下文的列表。

 调用[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)获取此接口表示一组特定的源文档中的所有代码上下文。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IEnumDebugCodeContexts2`。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|检索指定的数目的枚举序列中的代码上下文。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|跳过枚举序列中的代码上下文的指定的数目。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|将枚举序列重置到开头。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|获取一个枚举器中的代码上下文的数目。|

## <a name="remarks"></a>备注
 Visual Studio 调用[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)来填充的列表的代码上下文中的用户可以选择从时设置的下一个语句或显示源文件的反汇编。 多个代码上下文可以发生，例如，如果有多个实例的C++的样式模板。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)