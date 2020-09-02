---
title: IEnumDebugFields：： GetCount |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugFields::GetCount
helpviewer_keywords:
- IEnumDebugFields::GetCount method
ms.assetid: 3f471b40-4db3-49f7-b504-58b2476eef74
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f45cabbc9f95b41cbaabbdef1e3241bdfa7959d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199657"
---
# <a name="ienumdebugfieldsgetcount"></a>IEnumDebugFields::GetCount
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法返回枚举中的元素数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetCount(  
   [out] ULONG* pcelt  
);  
```  
  
```csharp  
int GetCount(  
   out uint pcelt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pcelt`  
 弄返回枚举中的元素数。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法不是习惯的 COM 枚举接口的一部分，它指定仅需实现下一个、克隆、跳过和重置。  
  
## <a name="see-also"></a>另请参阅  
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
