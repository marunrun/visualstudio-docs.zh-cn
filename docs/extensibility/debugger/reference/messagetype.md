---
title: MESSAGETYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c17860bb47f493031e6db1134aec498611b07f1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339197"
---
# <a name="messagetype"></a>MESSAGETYPE
指定消息类型和原因。

## <a name="syntax"></a>语法

```cpp
enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
typedef DWORD MESSAGETYPE;
```

```csharp
public enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
```

## <a name="fields"></a>字段
 `MT_OUTPUTSTRING`\
 指示应将消息发送到输出窗口。 这是互相排斥从`MT_MESSAGEBOX`。

 `MT_MESSAGEBOX`\
 指示应在消息框中显示的消息。 这是互相排斥从`MT_OUTPUTSTRING`。

 `MT_TYPE_MASK`\
 要隔离的消息目标的掩码值。

 `MT_REASON_EXCEPTION`\
 指示由于异常而显示一个消息框。 这是互相排斥从`MT_REASON_TRACEPOINT`。

 `MT_REASON_TRACEPOINT`\
 指示由于命中跟踪点显示一个消息框。 这是互斥的`MT_REASON_EXCEPTION`。

 `MT_REASON_MASK`\
 要隔离所显示的消息的原因的掩码值。

## <a name="remarks"></a>备注
 这些值返回从[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)并[GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)方法。

 一个原因值可以与一个输出目标值使用按位组合`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)