---
title: IDebugComPlusSymbolProvider2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider2 interface
ms.assetid: fa2f9b49-03ad-43c7-92d6-6dcb9c3d0531
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 868528d5fd7d54f0a515a32895646b0cb94b26ce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186481"
---
# <a name="idebugcomplussymbolprovider2"></a>IDebugComPlusSymbolProvider2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示具有特定于托管代码的方法的 COM + 符号提供程序和扩展**IDebugComPlusSymbolProvider**[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugComPlusSymbolProvider2 : IDebugComPlusSymbolProvider  
```  
  
## <a name="methods"></a>方法  
 除了上的方法[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[FunctionHasLineInfo](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-functionhaslineinfo.md)|确定指定的方法是否具有行信息。|  
|[GetTypesByName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-gettypesbyname.md)|检索在给定其名称的类型。|  
|[GetTypeFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-gettypefromtoken.md)|检索在给定其标记的类型。|  
|[IsAddressSequencePoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-isaddresssequencepoint.md)|确定指定的调试地址是序列点。|  
|[LoadSymbolsFromCallback](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromcallback.md)|加载调试符号使用指定的回调方法。|  
|[LoadSymbolsFromStreamWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromstreamwithcormodule.md)|从给定的数据流加载调试符号**icor 调试模块**对象。|  
|[LoadSymbolsWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolswithcormodule.md)|加载调试符号给定**icor 调试模块**对象。|  
  
## <a name="requirements"></a>要求  
 标头：Sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
