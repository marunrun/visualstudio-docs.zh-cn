---
title: IEnumCodePaths2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumCodePaths2
helpviewer_keywords:
- IEnumCodePaths2 interface
ms.assetid: 17ec9f9e-dc06-4532-b5db-da52efcc8630
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 577b2691ed67751407621d5000ee9a8abec318df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192006"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示的代码路径的列表。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumCodePaths2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口来表示一系列代码路径。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)若要获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumCodePaths2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|检索指定的数目的枚举序列中的代码路径。|  
|[Skip](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|将跳过指定的数目的枚举序列中的代码路径。|  
|[Reset](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|获取一个枚举器中的代码路径的数量。|  
  
## <a name="remarks"></a>备注  
 代码路径表示在程序中的分支点或函数调用。 一系列代码路径表示的代码执行已通过其所采用的路径。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
