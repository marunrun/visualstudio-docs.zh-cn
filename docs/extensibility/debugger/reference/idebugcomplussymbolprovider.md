---
title: IDebugComPlusSymbolProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider interface
ms.assetid: 5b98e908-fd15-49a6-9010-933c9b948085
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4388b3d561420282ade0104443e0db8061ef2ff6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352761"
---
# <a name="idebugcomplussymbolprovider"></a>IDebugComPlusSymbolProvider
表示 COM + 符号提供程序使用特定于托管代码的方法。

## <a name="syntax"></a>语法

```
IDebugComPlusSymbolProvider : IDebugSymbolProvider
```

## <a name="notes-for-implementers"></a>实施者的说明
 尽管没有对的表达式计算器 (EE) 都很有用的接口和用于由调试引擎 (DE) 之间没有分隔，但以下方法将可能感兴趣 DE 开发人员：AreSymbolsLoaded、 GetAddressesInModuleFromPosition、 GetEntryPoint、 GetFunctionLineOffset、 GetLocalVariableLayout、 IsFunctionStale、 LoadSymbols、 LoadSymbolsFromStream、 ReplaceSymbols、 UnloadSymbols 和 UpdateSymbols。

## <a name="methods"></a>方法
 除了上的方法[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)接口，此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[AreSymbolsLoaded](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-aresymbolsloaded.md)|确定是否为给定的应用程序域标识符的指定模块加载调试符号。|
|[CreateTypeFromPrimitive](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-createtypefromprimitive.md)|从指定的基元类型创建类型。|
|[GetAddressesInModuleFromPosition](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getaddressesinmodulefromposition.md)|将指定的模块中的文档位置映射到调试地址的数组。|
|[GetArrayTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getarraytypefromaddress.md)|检索类型信息指定给出其调试地址的数组。|
|[GetAssemblyName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getassemblyname.md)|检索给定其模块和应用程序域的程序集的名称。|
|[GetAttributedClassesForLanguage](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesforlanguage.md)|检索在给定的编程语言中实现与指定的特性的类。|
|[GetAttributedClassesinModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesinmodule.md)|检索与给定模块中的指定属性的类。|
|[GetEntryPoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getentrypoint.md)|检索应用程序入口点。|
|[GetFunctionLineOffset](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getfunctionlineoffset.md)|检索表示给定的行偏移量的函数内的地址。|
|[GetLocalVariablelayout](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getlocalvariablelayout.md)|检索一组方法的局部变量的布局。|
|[GetNameFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getnamefromtoken.md)|返回与给定其元数据对象的指定标记关联的名称。|
|[GetSymAttribute](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymattribute.md)|检索与给定的父属性指定模块的调试符号。|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymunmanagedreader.md)|检索要使用由非托管代码的符号读取器。|
|[GetTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-gettypefromaddress.md)|检索到给出其调试地址符号类型。|
|[IsFunctionDeleted](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctiondeleted.md)|确定是否删除指定的调试地址处的函数。|
|[IsFunctionStale](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctionstale.md)|确定是否在指定的调试地址函数被视为过时。|
|[IsHiddenCode](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-ishiddencode.md)|确定指定的调试程序地址处代码处于隐藏状态。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbols.md)|加载在内存中的指定的调试符号。|
|[LoadSymbolsFromStream](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbolsfromstream.md)|加载调试符号提供数据流。|
|[ReplaceSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-replacesymbols.md)|与指定的数据流中的替换当前的调试符号。|
|[UnloadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-unloadsymbols.md)|卸载从内存指定的模块的调试符号。|
|[UpdateSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-updatesymbols.md)|更新内存中的调试符号与指定的数据流。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll