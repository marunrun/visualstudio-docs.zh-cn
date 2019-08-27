---
title: CONNECTION_PROTOCOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONNECTION_PROTOCOL
helpviewer_keywords:
- CONNECTION_PROTOCOL enumeration
ms.assetid: 99df5865-8b36-486d-9f4c-d10ae2bc688a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3f52ef7e723b583d593f6f0d4fc18f5f6909b131
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346522"
---
# <a name="connectionprotocol"></a>CONNECTION_PROTOCOL
指示正在使用调试服务器和调试包 (DE) 之间进行通信的协议。

## <a name="syntax"></a>语法

```cpp
typedef enum tagCONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
} CONNECTION_PROTOCOL;
```

```csharp
public enum CONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
};
```

## <a name="fields"></a>字段
`CONNECTION_NONE`\
没有连接到服务器。

`CONNECTION_UNKNOWN`\
已建立连接，但它属于未知类型。

`CONNECTION_LOCAL`\
连接是连接到本地服务器。

`CONNECTION_PIPE`\
通过命名管道连接。

`CONNECTION_TCPIP`\
连接使用 TCP/IP。

`CONNECTION_HTTP`\
将使用 HTTP 连接 （通过 Web 服务器上）。

`CONNECTION_OTHER`\
已建立某种其他类型的连接 （此值当前未使用）。

## <a name="remarks"></a>备注
这些值返回从[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
