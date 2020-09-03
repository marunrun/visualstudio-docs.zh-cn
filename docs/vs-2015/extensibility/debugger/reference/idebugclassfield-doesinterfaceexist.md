---
title: IDebugClassField：:D oesInterfaceExist |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9f71346c1b69729ae54ef0d33be4149e7000316c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191126"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

确定是否在类中定义了特定接口。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT DoesInterfaceExist(   
   LPCOLESTR pszInterfaceName  
);  
```  
  
```csharp  
int DoesInterfaceExist(  
   [In] string pszInterfaceName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszInterfaceName`  
 中一个包含要查找的接口名称的字符串。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK，如果接口不存在，则返回 S_FALSE;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法有效地获取所有接口的枚举，并在列表中搜索匹配的接口。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
