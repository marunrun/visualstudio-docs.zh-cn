---
title: 符号提供程序接口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- interfaces, symbol handler
- symbol handler, interfaces
- symbol handler, evaluating variables
ms.assetid: 4201f10e-c9f7-4b38-bb45-40fe0082d5bf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec20da7f2860d2b74cde0286a8480d28738c0a31
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329153"
---
# <a name="symbol-provider-interfaces"></a>符号提供程序接口
以下是有关符号处理接口[!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)]。

## <a name="discussion"></a>讨论
 这些接口用于在中断模式下评估调用堆栈中的变量。 它们仅对公共语言运行时符号提供程序 (SP) 被实现。

|接口|由实现|描述|
|---------------|--------------------|-----------------|
|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)|SP|表示项的地址。|
|[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)|SP|表示地址的项，请访问进程 id。|
|[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)|SP|表示一个数组符号或数组类型。|
|[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)|SP|表示类符号或类类型。|
|[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)|SP|表示 COM + 符号提供程序使用特定于托管代码的方法。|
|[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)|SP|表示具有特定于托管代码的方法的 COM + 符号提供程序和扩展**IDebugComPlusSymbolProvider**。|
|[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)|SP|表示符号或其他符号或类型的容器类型。|
|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)|SP|表示可附加到一个符号的自定义属性。|
|[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)|SP|表示对方法或类型的自定义属性的查询。|
|[IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)|SP|提供对自定义属性的访问的符号。|
|[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)|SP|可以在运行时确定任何类型的基接口。|
|[IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)|SP|表示有关动态字段[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。|
|[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)|SP|表示一个枚举类型。|
|[IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)|sp|扩展可用字段以支持托管的代码的泛型的类型。|
|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)|SP|所有字段; 类的基类表示符号或类型的说明。|
|[IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)|SP|表示托管的代码的泛型类型的字段的定义。|
|[IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)|SP|表示托管的代码的泛型类型的字段的一个实例。|
|[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)|SP|表示托管的代码的泛型类型的参数。|
|[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)|SP|表示的方法。|
|[IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)|SP|表示调试可选修饰符。|
|[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)|SP|表示的指针。|
|[IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)|SP|表示基元类型枚举值从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口。|
|[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)|SP|表示可获取或设置一个托管的代码类的属性。|
|[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)|SP|表示提供了符号和类型的符号提供程序。|
|[IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)|SP|表示元数据和 core 符号接口符号提供程序的直接访问权限。|
|[IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)|SP|表示创建表示一种类型的字段的功能。|
|[IDebugTypeFieldBuilder2](../../../extensibility/debugger/reference/idebugtypefieldbuilder2.md)|SP|扩展了**IDebugTypeFieldBuilder**能够创建数组类型。|
|[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)|SP|表示一系列[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。|
|[IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)|SP|表示一系列[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)对象。|
|[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)|SP|表示一系列[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。|

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)