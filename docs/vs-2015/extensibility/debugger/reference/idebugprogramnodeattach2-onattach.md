---
title: IDebugProgramNodeAttach2::OnAttach | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 845ec66215c5d999aaf3b5c9658bc0fb8e7295a7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148547"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将附加到相关联的程序或将推迟到 attach 进程[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT OnAttach(  
   [in] REFGUID guidProgramId  
);  
```  
  
```csharp  
int OnAttach(  
   ref Guid guidProgramId  
};  
```  
  
#### <a name="parameters"></a>参数  
 `guidProgramId`  
 [in]`GUID`要分配给关联的程序。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)不应调用方法。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法之前调用在附加过程中，[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)调用方法。 `OnAttach`方法可以执行附加过程本身 (在这种情况下，此方法返回`S_FALSE`) 或推迟到附加过程`IDebugEngine2::Attach`方法 (`OnAttach`方法将返回`S_OK`)。 在既情况下，`OnAttach`方法可以设置`GUID`到正在调试的程序的给定`GUID`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
