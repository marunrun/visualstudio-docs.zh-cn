---
title: 实现表达式计算器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e82e6f1fb4e6f78c7fb1f614144f9a836d9676fb
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436360"
---
# <a name="implementing-an-expression-evaluator"></a>实现表达式计算器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 计算表达式是复杂叠加而在调试引擎 (DE)、 符号提供程序 (SP)、 联编程序对象和表达式计算器 (EE) 本身。 以下四个组件的接口是由一个组件实现和使用由另一个连接。  
  
 EE DE 中字符串的形式从所需的表达式和解析或对其进行计算。 EE 实现以下接口，供 DE:  
  
- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)  
  
- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)  
  
  EE 调用 DE，若要获取的符号和对象的值由提供的联编程序对象。 EE 使用由 DE 实现以下接口：  
  
- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)  
  
- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)  
  
- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)  
  
- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)  
  
- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)  
  
- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)  
  
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)  
  
  实现 EE [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)。 `IDebugProperty2` 提供用于描述结果的表达式计算，如本地变量、 基元或一个对象，Visual studio，然后显示中的相应信息的机制**局部变量**， **观看**，或**即时**窗口。  
  
  SP 时为指定 EE DE 通过要求提供的信息。 SP 实现接口，用于描述地址和字段，如下面的接口和及其衍生产品：  
  
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)  
  
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)  
  
- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)  
  
  EE 使用所有这些接口。  
  
## <a name="in-this-section"></a>本节内容  
 [表达式计算器实施策略](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)  
 定义了表达式计算器 (EE) 实施策略一个三步骤过程。  
  
## <a name="see-also"></a>请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
