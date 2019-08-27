---
title: IDebugExpressionEvaluator2::Terminate |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Terminate
- IDebugExpressionEvaluator2::Terminate
ms.assetid: 38265100-4d80-4902-833a-07bb569f9ba8
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3957728bf52e21a166abf3771d3cccf282c1c8da
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149002"
---
# <a name="idebugexpressionevaluator2terminate"></a>IDebugExpressionEvaluator2::Terminate
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

停止并清除表达式计算器。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Terminate (  
    void  
);  
```  
  
```csharp  
int Terminate ();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 指示表达式计算器时它正被清除。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于**ExpressionEvaluatorPackage**对象，它公开[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)接口。  
  
```cpp#  
STDMETHODIMP ExpressionEvaluatorPackage::Terminate(void)  
{  
    // scan the namespaces contained and delete  
    EEExtensionMethodCache **ppChild = NULL;  
    m_HashExtensionMethodCache.ResetHashIterator();  
    while (ppChild = m_HashExtensionMethodCache.IterateHash())  
    {  
        delete *ppChild;  
    }  
    return VBEEImplicitVariables::Terminate();  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
