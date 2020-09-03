---
title: IDebugModule3：： GetSymbolInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3aafb28715f58eaba4499b47a2e1dee15b82ed14
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80726899"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
检索搜索符号以及搜索每个路径的结果的路径列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymbolInfo(
    SYMBOL_SEARCH_INFO_FIELDS  dwFields,
    MODULE_SYMBOL_SEARCH_INFO* pInfo
);
```

```csharp
int GetSymbolInfo(
    enum_SYMBOL_SEARCH_INFO_FIELDS dwFields,
    MODULE_SYMBOL_SEARCH_INFO[]    pinfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
中 [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) 枚举中的标志的组合， `pInfo` 用于指定要填写的字段。

`pInfo`\
弄一个 [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 结构，其成员将使用指定的信息进行填充。 如果这是 null 值，则此方法返回 `E_INVALIDARG` 。

## <a name="return-value"></a>返回值
如果该方法成功，则返回 `S_OK` ; 否则返回错误代码。

> [!NOTE]
> `MODULE_SYMBOL_SEARCH_INFO`即使返回，结构) 中返回的字符串 (也可能为空 `S_OK` 。 在这种情况下，没有要返回的搜索信息。

## <a name="remarks"></a>备注
如果 `bstrVerboseSearchInfo` 结构的字段 `MODULE_SYMBOL_SEARCH_INFO` 不为空，则它包含搜索的路径列表和该搜索的结果。 该列表的格式为路径，后跟省略号 ( "..." ) ，然后是结果。 如果有多个路径结果对，则每个对都由 "\r\n" (回车/换行) 对分隔。 模式如下所示：

\<path>...\<result>\r\n \<path> ... \<result>\r\n \<path> .。。\<result>

请注意，最后一个条目没有 \r\n 序列。

## <a name="example"></a>示例
在此示例中，此方法返回三个路径，其中包含三个不同的搜索结果。 每行都以回车符/换行符对结尾。 示例输出只是以单个字符串的形式打印搜索结果。

> [!NOTE]
> 状态结果是紧跟在 "..."直到行的末尾。

```cpp
void ShowSymbolSearchResults(IDebugModule3 *pIDebugModule3)
{
    MODULE_SYMBOL_SEARCH_INFO ssi = { 0 };
    HRESULT hr;
    hr = pIDebugModule3->GetSymbolInfo(SSIF_VERBOSE_SEARCH_INFO,&ssi);
    if (SUCCEEDED(hr)) {
        CComBSTR searchInfo = ssi.bstrVerboseSearchInfo;
        if (searchInfo.Length() != 0) {
            std::wcout << (wchar_t *)(BSTR)searchInfo;
            std::wcout << std::endl;
        }
    }
}
```

**c:\symbols\user32.pdb.。。找不到文件。** 
**c:\winnt\symbols\user32.pdb.。。版本不匹配。** 
** \\\symbols\symbols\user32.dll \0a8sd0ad8ad\user32.pdb.。。已加载符号。**

## <a name="see-also"></a>另请参阅

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
