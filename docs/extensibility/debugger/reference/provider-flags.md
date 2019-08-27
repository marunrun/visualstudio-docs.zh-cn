---
title: PROVIDER_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_FLAGS
helpviewer_keywords:
- PROVIDER_FLAGS enumeration
ms.assetid: 8cbd2312-ed2f-4477-b192-c3f25c6098c3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8408481efbcaa67ce60d2dbfc9166b5dd0fd5223
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350027"
---
# <a name="providerflags"></a>PROVIDER_FLAGS
指定要从程序提供程序获取所需的属性。

## <a name="syntax"></a>语法

```cpp
enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
typedef DWORD PROVIDER_FLAGS;
```

```csharp
public enum enum_PROVIDER_FLAGS {
   PFLAG_NONE                    = 0x00,
   PFLAG_REMOTE_PORT             = 0x01,
   PFLAG_DEBUGGEE                = 0x02,
   PFLAG_ATTACHED_TO_DEBUGGEE    = 0x04,
   PFLAG_REASON_WATCH            = 0x08,
   PFLAG_GET_PROGRAM_NODES       = 0x10,
   PFLAG_GET_IS_DEBUGGER_PRESENT = 0x20
};
```

## <a name="fields"></a>字段
 `PFLAG_NONE`\
 指定任何标志。

 `PFLAG_REMOTE_PORT`\
 调用方想以外的其他计算机上的程序列表[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]。

 `PFLAG_DEBUGGEE`\
 进程当前正在调试的此实例[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]。

 `PFLAG_ATTACH_TODEBUGGEE`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 附加到正在调试的程序，但未启动。

 `PFLAG_REASON_WATCH`\
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 正在监视的事件。

 `PFLAG_GET_PROGRAM_NODES`\
 调用方想`ProgramNodes`字段[PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)结构。

 `PFLAG_GET_IS_DEBUGGER_PRESENT`\
 调用方想`fIsTheDebuggerPresent`字段的`PROVIDER_PROCESS_DATA`结构。

## <a name="remarks"></a>备注
 这些标志将传递到以下方法：

- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)

- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)

- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)

  可以组合这些值的按位`OR`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)