---
title: IDebugModule3::LoadSymbols |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugModule3::LoadSymbols
helpviewer_keywords:
- IDebugModule3::LoadSymbols
ms.assetid: 7548c8c1-cbc6-48aa-a845-19058d4a85bb
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 46385a61c5cc8cc30f75fd06a55bbe155e045f0a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157285"
---
# <a name="idebugmodule3loadsymbols"></a>IDebugModule3::LoadSymbols
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

加载当前模块的符号。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT LoadSymbols(  
   void  
);  
```  
  
```csharp  
int LoadSymbols();  
```  
  
## <a name="return-value"></a>返回值  
 如果此方法成功，它将返回`S_OK`。 如果失败，则返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法从当前的搜索路径加载符号 (这可以通过调用更改[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)方法)。  
  
 此方法是通过首选[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)   
 [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
