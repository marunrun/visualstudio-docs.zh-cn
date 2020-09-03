---
title: IDebugProgramHost2：： GetHostName |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramHost2::GetHostName
helpviewer_keywords:
- IDebugProgramHost2::GetHostName
ms.assetid: 48bbb089-e59a-471a-9965-24b42a8dabf3
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb7ceae40282115dc455691789c3882a1620e829
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68165128"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取此程序的宿主进程的标题、友好名称或文件名。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetHostName(   
   DWORD dwType,  
   BSTR* pbstrHostName  
);  
```  
  
```csharp  
int GetHostName(   
   uint dwType,  
   out string pbstrHostName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwType`  
 中 [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md) 枚举中的一个值。  
  
 `pbstrHostName`  
 弄返回宿主进程的请求的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 在此方法的典型实现中，将 `dwType` 忽略参数，并返回主机的友好名称。 另一种可能的实现方法是将 `dwType` 参数传递给 [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) 方法的调用以获取名称。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)   
 [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
