---
title: SymTagEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 806fe878468baa06b52a15879ceaff1b376461e9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738519"
---
# <a name="symtagenum"></a>SymTagEnum
指定符号的类型。

## <a name="syntax"></a>语法

```C++
enum SymTagEnum {
    SymTagNull,
    SymTagExe,
    SymTagCompiland,
    SymTagCompilandDetails,
    SymTagCompilandEnv,
    SymTagFunction,
    SymTagBlock,
    SymTagData,
    SymTagAnnotation,
    SymTagLabel,
    SymTagPublicSymbol,
    SymTagUDT,
    SymTagEnum,
    SymTagFunctionType,
    SymTagPointerType,
    SymTagArrayType,
    SymTagBaseType,
    SymTagTypedef,
    SymTagBaseClass,
    SymTagFriend,
    SymTagFunctionArgType,
    SymTagFuncDebugStart,
    SymTagFuncDebugEnd,
    SymTagUsingNamespace,
    SymTagVTableShape,
    SymTagVTable,
    SymTagCustom,
    SymTagThunk,
    SymTagCustomType,
    SymTagManagedType,
    SymTagDimension,
    SymTagCallSite,
    SymTagInlineSite,
    SymTagBaseInterface,
    SymTagVectorType,
    SymTagMatrixType,
    SymTagHLSLType
};
```

## <a name="elements"></a>元素
`SymTagNull` 指示该符号没有类型。

`SymTagExe` 指示该符号为 .exe 文件。 每个符号存储只有一个 `SymTagExe` 符号。 它充当全局范围，没有词法父项。

`SymTagCompiland` 指示符号存储区的每个编译单位组件的编译单位符号。 对于本机应用程序，`SymTagCompiland` 符号对应于链接到图像的对象文件。 对于某些类型的 Microsoft 中间语言（MSIL）映像，每个类都有一个编译单位。

`SymTagCompilandDetails` 指示该符号包含编译单位的扩展属性。 检索这些属性可能需要加载编译单位符号。

`SymTagCompilandEnv` 指示该符号是为编译单位定义的环境字符串。

`SymTagFunction` 指示该符号是一个函数。

`SymTagBlock` 指示该符号是嵌套块。

`SymTagData` 指示符号为 data。

`SymTagAnnotation` 指示符号适用于代码批注。 此符号的子级是常量数据字符串（`SymTagData`、`LocIsConstant` `DataIsConstant`）。 大多数客户端会忽略此符号。

`SymTagLabel` 指示该符号是一个标签。

`SymTagPublicSymbol` 指示符号为公共符号。 对于本机应用程序，此符号是链接图像时遇到的 COFF 外部符号。

`SymTagUDT` 指示该符号是用户定义的类型（结构、类或联合）。

`SymTagEnum` 指示符号为枚举。

`SymTagFunctionType` 指示该符号是函数签名类型。

`SymTagPointerType` 指示符号是指针类型。

`SymTagArrayType` 指示符号为数组类型。

`SymTagBaseType` 指示符号为基类型。

`SymTagTypedef` 指示符号是一个 `typedef`，即另一个类型的别名。

`SymTagBaseClass` 指示该符号是用户定义类型的基类。

`SymTagFriend` 指示该符号是用户定义类型的友元。

`SymTagFunctionArgType` 指示该符号是函数自变量。

`SymTagFuncDebugStart` 指示该符号是函数的序言代码的结束位置。

`SymTagFuncDebugEnd` 指示该符号是函数的尾声代码的起始位置。

`SymTagUsingNamespace` 指示符号是在当前范围内处于活动状态的命名空间名称。

`SymTagVTableShape` 指示符号为虚拟表说明。

`SymTagVTable` 指示符号为虚拟表指针。

`SymTagCustom` 指示该符号是一个自定义符号，不由 DIA 进行解释。

`SymTagThunk` 指示符号是用于在16到32位代码之间共享数据的 thunk。

`SymTagCustomType` 指示该符号是自定义编译器符号。

`SymTagManagedType` 指示符号在元数据中。

`SymTagDimension` 指示该符号为 FORTRAN 多维数组。

`SymTagCallSite` 指示符号表示调用站点。

`SymTagInlineSite` 指示符号表示内联站点。

`SymTagBaseInterface` 指示该符号是基接口。

`SymTagVectorType` 指示符号为矢量类型。

`SymTagMatrixType` 指示符号为矩阵类型。

`SymTagHLSLType` 指示该符号是高级着色器语言类型。

## <a name="remarks"></a>备注
调试文件中的所有符号都具有指定符号类型的标识标记。

此枚举中的值由对[IDiaSymbol：： get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)方法的调用返回。

此枚举中的值将传递给以下方法，以将搜索范围限制为特定的符号类型：

- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)

- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)

- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)

- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)

- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)

- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)

- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)

- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
