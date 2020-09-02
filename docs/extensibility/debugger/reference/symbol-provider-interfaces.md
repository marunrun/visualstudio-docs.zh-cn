---
title: 符号提供程序接口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- interfaces, symbol handler
- symbol handler, interfaces
- symbol handler, evaluating variables
ms.assetid: 4201f10e-c9f7-4b38-bb45-40fe0082d5bf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7929ba36c76f0db1cabab087afe3590de509efff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715841"
---
# <a name="symbol-provider-interfaces"></a>符号提供程序接口
下面是的符号处理接口 [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] 。

## <a name="discussion"></a>讨论 (Discussion)
 这些接口用于在中断模式期间计算调用堆栈中的变量。 它们仅实现公共语言运行时符号提供程序 (SP) 。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)|SP|表示项的地址。|
|[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)|SP|表示项的地址，提供对进程 ID 的访问。|
|[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)|SP|表示数组符号或数组类型。|
|[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)|SP|表示类符号或类类型。|
|[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)|SP|表示一个 COM + 符号提供程序，其中包含特定于托管代码的方法。|
|[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)|SP|表示一个 COM + 符号提供程序，其中包含特定于托管代码并扩展 **IDebugComPlusSymbolProvider**的方法。|
|[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)|SP|表示作为其他符号或类型的容器的符号或类型。|
|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)|SP|表示可以附加到符号的自定义特性。|
|[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)|SP|表示对方法或类型的自定义特性的查询。|
|[IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)|SP|提供对符号上的自定义特性的访问。|
|[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)|SP|可在运行时确定的任何类型的基接口。|
|[IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)|SP|表示 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 对象的动态字段。|
|[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)|SP|表示枚举类型。|
|[IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)|Sp|扩展可用字段的类型以支持托管代码泛型。|
|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)|SP|所有字段的基类;表示符号或类型的说明。|
|[IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)|SP|表示托管代码泛型类型的字段定义。|
|[IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)|SP|表示托管代码泛型类型的字段的实例。|
|[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)|SP|表示托管代码泛型类型的参数。|
|[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)|SP|表示方法。|
|[IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)|SP|表示调试可选修饰符。|
|[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)|SP|表示指针。|
|[IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)|SP|表示 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口中的基元类型枚举值。|
|[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)|SP|表示可以获取或设置的托管代码类的属性。|
|[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)|SP|表示提供符号和类型的符号提供程序。|
|[IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)|SP|表示一个符号提供程序，该提供程序可直接访问元数据和核心符号接口。|
|[IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)|SP|表示创建表示类型的字段的功能。|
|[IDebugTypeFieldBuilder2](../../../extensibility/debugger/reference/idebugtypefieldbuilder2.md)|SP|扩展 **IDebugTypeFieldBuilder** ，以便能够创建数组类型。|
|[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)|SP|表示 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象的集合。|
|[IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)|SP|表示 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) 对象的集合。|
|[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)|SP|表示 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象的集合。|

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
