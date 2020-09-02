---
title: IDebugCustomAttribute：： GetName |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetName
helpviewer_keywords:
- IDebugCustomAttribute::GetName
ms.assetid: ba509cc5-5816-4925-a094-4c72d88c360c
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4463fc4f9d321b26487e885255843a7acd945f76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62569265"
---
# <a name="idebugcustomattributegetname"></a>IDebugCustomAttribute::GetName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取自定义属性的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetName(   
   BSTR* bstrName  
);  
```  
  
```csharp  
int GetName(  
   out string bstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `bstrName`  
 弄返回一个字符串，该字符串包含自定义特性的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法返回的命名对应于用于声明特性的类的名称。 这与自定义特性类本身的名称可能并不完全一致，因为 c # 允许在声明中使用自定义属性名称时将其从自定义属性名称中删除。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
