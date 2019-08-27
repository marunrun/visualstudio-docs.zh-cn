---
title: IDebugAlias | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6c05b6987804681176abdde0e8c94a7463a9163c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442304"
---
# <a name="idebugalias"></a>IDebugAlias
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 表示变量的数值别名。 别名是只是不同的名称的变量。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugAlias : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 表达式计算器 (EE) 实现此接口以支持变量数字别名。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)为特定对象创建一个别名。 若要搜索的别名，请使用[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)或[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 以下方法定义中`IDebugAlias`接口。  
  
|方法|描述|  
|------------|-----------------|  
|[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|获取此别名所引用的对象。|  
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|获取别名名称。|  
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|检索`ICorDebugValue`提供对访问接口的托管代码信息有关此对象 （仅适用于托管代码）。|  
|[Dispose](../../../extensibility/debugger/reference/idebugalias-dispose.md)|将此标记别名为不再使用。|  
  
## <a name="remarks"></a>备注  
 别名是以字符串形式的 # 字符，例如 1001 # 后跟一个十进制数。  
  
## <a name="requirements"></a>要求  
 标头： ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)   
 [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)   
 [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
