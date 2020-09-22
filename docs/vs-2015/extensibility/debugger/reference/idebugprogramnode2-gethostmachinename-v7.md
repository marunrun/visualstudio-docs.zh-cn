---
title: IDebugProgramNode2：： GetHostMachineName_V7 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
ms.assetid: a992f2c9-f68b-4146-8cc2-027753bf7ce6
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 63e4f1a3621dde3fba5e8a2dabf45eaceb5d8ea4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840572"
---
# <a name="idebugprogramnode2gethostmachinename_v7"></a>IDebugProgramNode2::GetHostMachineName_V7
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

弃用. 请勿使用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetHostMachineName_V7 (   
   BSTR* pbstrHostMachineName  
);  
```  
  
```csharp  
int GetHostMachineName_V7 (   
   out string pbstrHostMachineName  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pbstrHostMachineName`  
 弄返回正在运行程序的计算机的名称。  
  
## <a name="return-value"></a>返回值  
 实现应总是返回 `E_NOTIMPL` 。  
  
## <a name="remarks"></a>备注  
  
> [!WARNING]
> 在 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 中，不再使用此方法并且应总是返回 `E_NOTIMPL` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
