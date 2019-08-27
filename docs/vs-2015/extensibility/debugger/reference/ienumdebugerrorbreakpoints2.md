---
title: IEnumDebugErrorBreakpoints2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugErrorBreakpoints2
helpviewer_keywords:
- IEnumDebugErrorBreakpoints2
ms.assetid: ffdad73d-969a-45ef-9ad1-7f5d3b814018
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 95d001c0072442d07ae12f773a26290a95a2f7f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178474"
---
# <a name="ienumdebugerrorbreakpoints2"></a>IEnumDebugErrorBreakpoints2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举与挂起断点关联的错误断点。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugErrorBreakpoints2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口作为断点的支持的一部分。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 Visual Studio 调用[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)若要获取此界面表示无法绑定断点的列表或[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)若要获取此界面表示断点的列表未绑定的。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugErrorBreakpoints2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)|检索指定的数量的错误枚举序列中的断点。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-skip.md)|将跳过指定的数目的错误枚举序列中的断点。|  
|[Reset](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-getcount.md)|获取一个枚举器中的错误断点数。|  
  
## <a name="remarks"></a>备注  
 此接口包含一系列[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)接口，其中每个描述的断点无法绑定，以及为什么它无法绑定。 Visual Studio 将使用`IEnumDebugErrorBreakpoint2`接口以更新显示在 IDE 中的断点。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)   
 [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)   
 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
