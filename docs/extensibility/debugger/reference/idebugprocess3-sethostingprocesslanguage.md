---
title: IDebugProcess3::SetHostingProcessLanguage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::SetHostingProcessLanguage
helpviewer_keywords:
- IDebugProcess3::SetHostingProcessLanguage
ms.assetid: e42f33ed-f29c-4e45-92ce-ab504b72d77c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 242f35dce9245406c3466784811d79ac1942c49f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313912"
---
# <a name="idebugprocess3sethostingprocesslanguage"></a>IDebugProcess3::SetHostingProcessLanguage
此方法设置过程将托管下的语言。 此语言然后可通过调试引擎 (DE) 加载适当的表达式计算器。

## <a name="syntax"></a>语法

```cpp
HRESULT SetHostingProcessLanguage(
   REFGUID guidLang
);
```

```csharp
int SetHostingProcessLanguage(
   ref Guid guidLang
);
```

## <a name="parameters"></a>参数
`guidLang`\
[in]`GUID` DE 应使用的语言。 指定`GUID_NULL`(C++) 或`Guid.Empty`(C#) 能够使用的默认语言 DE。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="remarks"></a>备注
- [GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)可用于检索当前语言设置。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)