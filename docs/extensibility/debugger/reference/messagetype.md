---
title: 消息类型 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4d0fd12495a59427500c16ef6f37d9f8b6e61f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714487"
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
 指示应将消息发送到输出窗口。 这是来自`MT_MESSAGEBOX`的相互排斥。

 `MT_MESSAGEBOX`\
 指示消息应显示在消息框中。 这是来自`MT_OUTPUTSTRING`的相互排斥。

 `MT_TYPE_MASK`\
 用于隔离消息目标的掩码值。

 `MT_REASON_EXCEPTION`\
 指示消息框由于异常而显示。 这是来自`MT_REASON_TRACEPOINT`的相互排斥。

 `MT_REASON_TRACEPOINT`\
 指示由于命中跟踪点而显示消息框。 这是相互排斥的`MT_REASON_EXCEPTION`。

 `MT_REASON_MASK`\
 用于隔离显示消息原因的掩码值。

## <a name="remarks"></a>备注
 这些值从[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)和[GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)方法返回。

 其中一个原因值可以使用位值`OR`与输出目标值之一组合。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
