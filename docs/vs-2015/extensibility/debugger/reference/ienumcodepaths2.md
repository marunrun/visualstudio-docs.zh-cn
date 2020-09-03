---
title: IEnumCodePaths2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192006"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示代码路径的列表。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumCodePaths2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎 (DE) 实现此接口以表示代码路径的列表。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调用 [EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md) 以获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IEnumCodePaths2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|检索枚举序列中指定数目的代码路径。|  
|[Skip](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|跳过枚举序列中指定数目的代码路径。|  
|[重置](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|将枚举序列重置到开始处。|  
|[克隆](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|  
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|获取枚举器中的代码路径数。|  
  
## <a name="remarks"></a>备注  
 代码路径表示程序中的分支点或函数调用。 代码路径列表表示执行代码所用的路径。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
