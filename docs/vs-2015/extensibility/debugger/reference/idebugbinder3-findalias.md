---
title: IDebugBinder3：： FindAlias |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 47aaaec73d2c364e974b7430335404bf8caf406c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68142964"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法在给定名称的情况下查找别名。 这会搜索程序中的所有别名。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT FindAlias(  
   LPCOLESTR     pcstrName,  
   IDebugAlias** ppAlias  
);  
```  
  
```csharp  
int FindAlias(  
   string          pcstrName,  
   out IDebugAlias ppAlias  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pcstrName`  
 中要查找的别名的名称。  
  
 `ppAlias`  
 弄如果 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 接口所表示的任何)  (，则会找到别名。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则， `S_FALSE` 如果找不到别名) 或错误代码，则返回 (。  
  
## <a name="remarks"></a>备注  
 此方法在调用之前将目标对象初始化为 null;然后，它将在此后测试 null 值，以确定是否找到了别名。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)   
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
