---
title: IDebugCodeContext2::GetLanguageInfo |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugCodeContext2::GetLanguageInfo
ms.assetid: 03002ef1-9fe6-44b6-b23b-ef7b86b2b21b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0df2a08dd7906b9c4c0935d90150037a3bc0275a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190937"
---
# <a name="idebugcodecontext2getlanguageinfo"></a>IDebugCodeContext2::GetLanguageInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取此代码的上下文的语言信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
  
#### <a name="parameters"></a>参数  
 `pbstrLanguage`  
 [in、 out]返回一个字符串，例如包含的语言的名称"C++。"  
  
 `pguidLanguage`  
 [in、 out]例如，返回的语言的代码上下文，GUID `guidCPPLang`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 在至少一个参数必须返回非 null 值。  
  
## <a name="see-also"></a>请参阅  
 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
