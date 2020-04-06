---
title: MODULE_SYMBOL_SEARCH_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f15587759c4f665d1593d1298c47459a0e64aac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714240"
---
# <a name="module_symbol_search_info"></a>MODULE_SYMBOL_SEARCH_INFO

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
[SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)枚举中的标志的组合，指定此结构中描述的搜索信息类型。

`bstrVerboseSearchInfo`\
搜索路径和结果串联到单个字符串中。

## <a name="remarks"></a>备注

此结构从对[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)方法的调用返回。

如果`bstrVerboseSearchInfo`该字段不为空，则它包含搜索的路径列表和该搜索的结果。 列表的格式采用路径，后跟省略号 （"..."），后跟结果。 如果有多个路径结果对，则每对由一对"\r\n"（回车/换行）对分隔。 模式如下所示：

\<路径>...\<结果>\r\n\<路径>...\<结果>\r\n\<路径>...\<结果>

请注意，最后一个条目没有 \r\n 序列。

下面是已发送到标准`bstrVerboseSearchInfo`出的可能的字符串。

`c:\symbols\user32.pdb... File not found.`

`c:\winnt\symbols\user32.pdb... Version does not match.`

`\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`

## <a name="requirements"></a>要求

标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)
