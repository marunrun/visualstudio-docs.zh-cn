---
title: IDebugStackFrame2::GetLanguageInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetLanguageInfo
helpviewer_keywords:
- IDebugStackFrame2::GetLanguageInfo
ms.assetid: 0e12fd92-f155-46a7-8272-cda279388cfb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0318f99d234309093717c9603ec1153e71d6d7f3
ms.sourcegitcommit: 74c5360186731de07828764eb32ea1033a8c2275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67559701"
---
# <a name="idebugstackframe2getlanguageinfo"></a>IDebugStackFrame2::GetLanguageInfo

获取与此堆栈帧关联的语言。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLanguageInfo ( 
   BSTR* pbstrLanguage,
   GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo ( 
   ref string pbstrLanguage,
   ref Guid   pguidLanguage
);
```

## <a name="parameters"></a>参数

`pbstrLanguage`\
[out]返回的语言的实现与此堆栈帧关联的方法的名称。

`pguidLanguage`\
[out]返回`GUID`的语言。 有关[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]语言，例如，以下可返回：

- `guidVBScriptLang`\

- `guidJScriptLang`\

- `guidCPPLang`\

- `guidVBLang`\

- `guidSQLLang`\

- `guidScriptLang`\

## <a name="return-value"></a>返回值

 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅

- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
