---
title: IDebugSettingsCallback2：： GetEELocalObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEELocalObject
ms.assetid: e69a3469-a049-420c-b918-c48a1e7b9baf
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7e6bf186d8b4bf660cc4a22e962754e859378674
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202480"
---
# <a name="idebugsettingscallback2geteelocalobject"></a>IDebugSettingsCallback2::GetEELocalObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

根据给定的指标名称检索表达式计算器本地对象。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetEELocalObject(  
   REFGUID     guidLang,  
   REFGUID     guidVendor,  
   LPCWSTR     pszMetric,  
   IUnknown ** ppUnk  
);  
```  
  
```csharp  
private int GetEELocalObject(  
   ref Guid          guidLang,  
   ref Guid          guidVendor,  
   string            pszMetric,  
   out System.Object ppUnk  
);  
```  
  
#### <a name="parameters"></a>参数  
 `guidLang`  
 中编程语言的唯一标识符。  
  
 `guidVendor`  
 中供应商的唯一标识符。  
  
 `pszMetric`  
 中度量值的名称。  
  
 `ppUnk`  
 弄返回表达式计算器本地对象。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
