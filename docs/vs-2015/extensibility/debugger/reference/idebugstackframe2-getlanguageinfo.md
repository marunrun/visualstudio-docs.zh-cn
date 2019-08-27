---
title: IDebugStackFrame2::GetLanguageInfo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetLanguageInfo
helpviewer_keywords:
- IDebugStackFrame2::GetLanguageInfo
ms.assetid: 0e12fd92-f155-46a7-8272-cda279388cfb
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d370670ed86ee3484243fe5dc7cfdd8ea64be084
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153128"
---
# <a name="idebugstackframe2getlanguageinfo"></a>IDebugStackFrame2::GetLanguageInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取与此堆栈帧关联的语言。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
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
  
#### <a name="parameters"></a>参数  
 `pbstrLanguage`  
 [out]返回的语言的实现与此堆栈帧关联的方法的名称。  
  
 `pguidLanguage`  
 [out]返回`GUID`的语言。 有关[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]语言，例如，以下可返回：  
  
- `guidVBScriptLang`  
  
- `guidJScriptLang`  
  
- `guidCPPLang`  
  
- `guidVBLang`  
  
- `guidSQLLang`  
  
- `guidScriptLang`  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
