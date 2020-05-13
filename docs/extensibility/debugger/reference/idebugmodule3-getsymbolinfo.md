---
title: IDebugmodule3：：获取符号信息 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726899"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
检索搜索符号的路径列表以及搜索每个路径的结果。

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
[在][SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)枚举中的标志的组合，指定要填充哪些`pInfo`字段。

`pInfo`\
[出][一个MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)结构，其成员要用指定的信息填充。 如果这是 null 值，则此方法将返回`E_INVALIDARG`。

## <a name="return-value"></a>返回值
如果方法成功，它将返回`S_OK`。否则，它将返回一个错误代码。

> [!NOTE]
> 即使`S_OK`返回，返回的字符串`MODULE_SYMBOL_SEARCH_INFO`（在结构中）也可能为空。 在这种情况下，没有要返回的搜索信息。

## <a name="remarks"></a>备注
`bstrVerboseSearchInfo`如果`MODULE_SYMBOL_SEARCH_INFO`结构字段不为空，则它包含搜索的路径列表和该搜索的结果。 列表的格式采用路径，后跟省略号 （"..."），后跟结果。 如果有多个路径结果对，则每对由一对"\r\n"（回车/换行）对分隔。 模式如下所示：

\<路径>...\<结果>\r\n\<路径>...\<结果>\r\n\<路径>...\<结果>

请注意，最后一个条目没有 \r\n 序列。

## <a name="example"></a>示例
在此示例中，此方法返回三个具有三个不同搜索结果的路径。 每行都用回车/换行对终止。 示例输出将搜索结果打印为单个字符串。

> [!NOTE]
> 状态结果是"..."到行的末尾。

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

**c：\符号\用户32.pdb...找不到文件。**
 **c：\winnt\符号\user32.pdb...版本不匹配。**
[符号 **]符号\user32.dll_0a8sd0ad8ad_user32.pdb... \\已加载符号。**

## <a name="see-also"></a>请参阅

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
