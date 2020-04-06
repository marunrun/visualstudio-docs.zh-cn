---
title: IDebugComPlus符号提供程序2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider2 interface
ms.assetid: fa2f9b49-03ad-43c7-92d6-6dcb9c3d0531
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 28c68398b69196f53c4f8792f3479d403cbebcda
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733244"
---
# <a name="idebugcomplussymbolprovider2"></a>IDebugComPlusSymbolProvider2
表示 COM+ 符号提供程序，其方法特定于托管代码，并扩展**IDebugComPlusSymbol 提供程序**[IDebugComPlusSymbol提供程序](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)。

## <a name="syntax"></a>语法

```
IDebugComPlusSymbolProvider2 : IDebugComPlusSymbolProvider
```

## <a name="methods"></a>方法
 除了[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[FunctionHasLineInfo](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-functionhaslineinfo.md)|确定指定方法是否具有行信息。|
|[GetTypesByName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-gettypesbyname.md)|检索给定其名称的类型。|
|[GetTypeFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-gettypefromtoken.md)|检索给定其令牌的类型。|
|[IsAddressSequencePoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-isaddresssequencepoint.md)|确定指定的调试地址是否为序列点。|
|[LoadSymbolsFromCallback](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromcallback.md)|使用指定的回调方法加载调试符号。|
|[LoadSymbolsFromStreamWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolsfromstreamwithcormodule.md)|给定**ICorDebugModule**对象的数据流加载调试符号。|
|[LoadSymbolsWithCorModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2-loadsymbolswithcormodule.md)|加载给定**ICorDebugModule**对象的调试符号。|

## <a name="requirements"></a>要求
 标题： Sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
