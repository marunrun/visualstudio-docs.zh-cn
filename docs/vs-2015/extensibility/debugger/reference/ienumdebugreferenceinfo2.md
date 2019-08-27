---
title: IEnumDebugReferenceInfo2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2
helpviewer_keywords:
- IEnumDebugReferenceInfo2
ms.assetid: 7ed01441-686f-4032-8268-a4c750f19f85
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 21c39c553a153707bad707d50cf5a13ae87973fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147752"
---
# <a name="ienumdebugreferenceinfo2"></a>IEnumDebugReferenceInfo2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugReferenceInfo2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 在内存中实现此接口作为对对象的引用的支持的一部分。 仅当支持引用，必须实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 Visual Studio 调用[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)若要获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugReferenceInfo2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)|检索指定的数目的[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)枚举序列中的结构。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-skip.md)|跳过指定的数目的[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)枚举序列中的结构。|  
|[Reset](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-getcount.md)|获取数[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)枚举器中的结构。|  
  
## <a name="remarks"></a>备注  
 引用是实质上是一种类型和地址，而属性是名称、 类型和地址。 引用仍然存在，只要引用要存在于内存中的对象。 请参阅[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)的更多详细信息。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
