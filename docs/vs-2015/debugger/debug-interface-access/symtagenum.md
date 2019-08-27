---
title: SymTagEnum | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTagEnum enumeration
ms.assetid: 528a50cf-e13d-46ec-a98c-323d5d047de9
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1578d88265769414f68964e28d3426ffcc62f9e8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193517"
---
# <a name="symtagenum"></a>SymTagEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定符号的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum SymTagEnum {   
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
 `SymTagNull`  
 指示符号具有任何类型。  
  
 `SymTagExe`  
 表示符号是.exe 文件。 只有一个`SymTagExe`每个符号存储区的符号。 它可作为全局作用域并没有词法父级。  
  
 `SymTagCompiland`  
 表示符号存储区的每个编译单位组件编译单位符号。 对于本机应用程序，`SymTagCompiland`符号对应于对象文件链接到该映像。 对于某些类型的 Microsoft 中间语言 (MSIL) 映像，还有一个编译单位，每个类。  
  
 `SymTagCompilandDetails`  
 指示该符号包含扩展的属性的编译单位。 检索这些属性可能需要加载编译单位符号。  
  
 `SymTagCompilandEnv`  
 表示符号是可编译单位为定义的环境字符串。  
  
 `SymTagFunction`  
 指示该符号是一个函数。  
  
 `SymTagBlock`  
 表示符号是嵌套的块。  
  
 `SymTagData`  
 指示符号数据。  
  
 `SymTagAnnotation`  
 指示符号的代码注释。 此符号的子级是连续的数据的字符串 (`SymTagData`， `LocIsConstant`， `DataIsConstant`)。 大多数客户端忽略此符号。  
  
 `SymTagLabel`  
 表示符号是一个标签。  
  
 `SymTagPublicSymbol`  
 表示符号是公共符号。 对于本机应用程序，该符号是链接映像时遇到的 COFF 外部符号。  
  
 `SymTagUDT`  
 表示符号是用户定义类型 （结构、 类或联合）。  
  
 `SymTagEnum`  
 指示该符号是一个枚举。  
  
 `SymTagFunctionType`  
 表示符号是函数签名类型。  
  
 `SymTagPointerType`  
 表示符号是指针类型。  
  
 `SymTagArrayType`  
 表示符号是数组类型。  
  
 `SymTagBaseType`  
 表示符号是基类型。  
  
 `SymTagTypedef`  
 表示符号是`typedef`，另一种类型的别名。  
  
 `SymTagBaseClass`  
 表示符号是用户定义类型的基类。  
  
 `SymTagFriend`  
 表示符号是用户定义类型的友元。  
  
 `SymTagFunctionArgType`  
 指示该符号是函数的参数。  
  
 `SymTagFuncDebugStart`  
 表示符号是函数的序言代码的结束位置。  
  
 `SymTagFuncDebugEnd`  
 表示符号是函数的尾声代码的开始位置。  
  
 `SymTagUsingNamespace`  
 表示符号是当前作用域中处于活动状态的命名空间名称。  
  
 `SymTagVTableShape`  
 表示符号是虚拟表说明。  
  
 `SymTagVTable`  
 表示符号是一个虚拟表指针。  
  
 `SymTagCustom`  
 指示该符号是一个自定义的符号和 dia 时不会解释  
  
 `SymTagThunk`  
 表示符号是可用于 16 和 32 位代码之间共享数据的转换 （thunk）。  
  
 `SymTagCustomType`  
 表示符号是可自定义编译器符号。  
  
 `SymTagManagedType`  
 表示符号是在元数据中。  
  
 `SymTagDimension`  
 表示符号是 FORTRAN 多维数组。  
  
 `SymTagCallSite`  
 指示该符号表示调用站点。  
  
 `SymTagInlineSite`  
 指示该符号表示内联站点。  
  
 `SymTagBaseInterface`  
 表示符号是基接口。  
  
 `SymTagVectorType`  
 表示符号是矢量类型。  
  
 `SymTagMatrixType`  
 表示符号是矩阵类型。  
  
 `SymTagHLSLType`  
 表示符号是高级别着色器语言类型。  
  
## <a name="remarks"></a>备注  
 调试文件中的所有符号都有一个标识标记的指定符号的类型。  
  
 此枚举中的值返回通过调用[idiasymbol:: Get_symtag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)方法。  
  
 此枚举中的值传递到以下方法来限制对特定符号类型的搜索作用域：  
  
- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)  
  
- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)  
  
- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)  
  
- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)  
  
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)  
  
- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)  
  
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)  
  
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)  
  
## <a name="requirements"></a>要求  
 标头： cvconst.h  
  
## <a name="see-also"></a>请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)   
 [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)   
 [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)   
 [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)   
 [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)   
 [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)   
 [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
