---
title: IDebugCodeContext2::GetLanguageInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugCodeContext2::GetLanguageInfo
ms.assetid: 03002ef1-9fe6-44b6-b23b-ef7b86b2b21b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08138fcd67e7d4fd5115ac13fe1b8348f76245d8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339018"
---
# <a name="idebugcodecontext2getlanguageinfo"></a>IDebugCodeContext2::GetLanguageInfo
获取此代码的上下文的语言信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLanguageInfo( 
   BSTR* pbstrLanguage,
   GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo( 
   ref string pbstrLanguage,
   ref Guid pguidLanguage
);
```

## <a name="parameters"></a>参数
`pbstrLanguage`\
[in、 out]返回一个字符串，例如包含的语言的名称"C++。"

`pguidLanguage`\
[in、 out]例如，返回的语言的代码上下文，GUID `guidCPPLang`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 在至少一个参数必须返回非 null 值。

## <a name="see-also"></a>请参阅
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)