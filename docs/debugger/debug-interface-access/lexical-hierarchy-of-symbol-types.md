---
title: 符号类型的词法层次结构 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], type hierarchies
ms.assetid: 912da653-ddfe-45a4-84aa-64281283739a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f4b2e6fc0b24cc96f617e7b78c6bdcc59ddc5c0d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63399405"
---
# <a name="lexical-hierarchy-of-symbol-types"></a>符号类型的词法层次结构
下表显示了词法层次结构中的符号类型。

## <a name="symbol-types"></a>符号类型

|符号类型|描述|
|-----------------|-----------------|
|[批注](../../debugger/debug-interface-access/annotation.md)|在程序代码中指定带批注的位置。|
|[块](../../debugger/debug-interface-access/block.md)|在函数中指定嵌套作用域。|
|`Compiland`|指定`compiland`链接到.exe 文件。|
|[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)|指定编译单位数据可能需要加载其他编译单位的详细信息，因此会产生开销运行时检索。|
|[CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)|指定编译的编译单位对任何其他环境变量。|
|[自定义（调试接口访问 SDK）](../../debugger/debug-interface-access/custom-debug-interface-access-sdk.md)|指定用户定义的符号。|
|[数据（调试界面访问 SDK）](../../debugger/debug-interface-access/data-debug-interface-access-sdk.md)|指定此类变量作为参数、 局部变量、 全局变量和类成员。|
|[Exe](../../debugger/debug-interface-access/exe.md)|指定全局范围的数据;对应于整个.exe 或.dll 文件。|
|[FuncDebugEnd](../../debugger/debug-interface-access/funcdebugend.md)|指定已定义的点的函数的调试是结束。|
|[FuncDebugStart](../../debugger/debug-interface-access/funcdebugstart.md)|指定已定义的点的函数的调试是开始。|
|[函数（调试接口访问 SDK）](../../debugger/debug-interface-access/function-debug-interface-access-sdk.md)|指定的函数。|
|[标签（调试接口访问 SDK）](../../debugger/debug-interface-access/label-debug-interface-access-sdk.md)|在程序代码中指定的位置。|
|[PublicSymbol](../../debugger/debug-interface-access/publicsymbol.md)|指定生成可执行程序时，将显示的外部符号。|
|[Thunk](../../debugger/debug-interface-access/thunk.md)|指定`thunk`。|
|[UsingNameSpace](../../debugger/debug-interface-access/usingnamespace.md)|指定`namespace`标识符。|

> [!NOTE]
> 其他符号属性可能可用，具体取决于符号类型。 单个符号主题中列出了这些属性。

## <a name="see-also"></a>请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
- [符号和符号标记](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)