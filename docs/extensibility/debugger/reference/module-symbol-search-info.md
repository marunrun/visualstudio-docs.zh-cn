---
title: MODULE_SYMBOL_SEARCH_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c521ebe321813013b83a951d4d2aa5f60fd1646d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346619"
---
# <a name="modulesymbolsearchinfo"></a>MODULE_SYMBOL_SEARCH_INFO

包含有关已搜索的符号搜索路径的状态信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagSYMBOL_SEARCH_INFO
{
    SYMBOL_SEARCH_INFO_FIELDS dwValidFields;
    BSTR                      bstrVerboseSearchInfo;
} MODULE_SYMBOL_SEARCH_INFO;
```

```csharp
public struct MODULE_SYMBOL_SEARCH_INFO {
    public uint   dwValidFields;
    public string bstrVerboseSearchInfo;
}
```

## <a name="members"></a>成员

`dwValidFields`\
中的标志的组合[SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)枚举，它指定此结构中所述的搜索信息的类型。

`bstrVerboseSearchInfo`\
搜索路径和结果连接成单个字符串。

## <a name="remarks"></a>备注

此结构从调用返回[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)方法。

如果`bstrVerboseSearchInfo`字段不为空，则它包含搜索路径和该搜索的结果的列表。 列表格式与跟省略号 （"..."） 后, 跟结果的路径。 如果有多个路径结果对，然后由"\r\n"（回车符-/ 换行） 对分隔每个对。 该模式如下所示：

\<path>...\<result>\r\n\<path>...\<result>\r\n\<path>...\<result>

请注意，最后一项没有 \r\n 序列。

下面是可能发生`bstrVerboseSearchInfo`已发送到标准输出的字符串。

`c:\symbols\user32.pdb... File not found.`

`c:\winnt\symbols\user32.pdb... Version does not match.`

`\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`

## <a name="requirements"></a>要求

标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)