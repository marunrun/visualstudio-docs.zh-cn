---
title: AD_PROCESS_ID_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d471a73205383f0f23c5016872712a3ba2c578d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153615"
---
# <a name="adprocessidtype"></a>AD_PROCESS_ID_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定如何解释中的进程 ID [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
typedef DWORD AD_PROCESS_ID_TYPE;  
```  
  
```csharp  
public enum enum_AD_PROCESS_ID {  
   AD_PROCESS_ID_SYSTEM = 0,  
   AD_PROCESS_ID_GUID   = 1  
};  
```  
  
## <a name="members"></a>成员  
 AD_PROCESS_ID_SYSTEM  
 进程 ID 是系统标识符。 使用`ProcessId.dwProcessId`字段[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构。  
  
 AD_PROCESS_ID_GUID  
 进程 ID 是一个 GUID。 使用`ProcessId.guidProcessId`字段的`AD_PROCESS_ID`结构。  
  
## <a name="remarks"></a>备注  
 用于`ProcessIdType`的成员[AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)结构以确定结构中包含的进程 ID 的类型。 确定如何解释`ProcessId`联合结构中。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
