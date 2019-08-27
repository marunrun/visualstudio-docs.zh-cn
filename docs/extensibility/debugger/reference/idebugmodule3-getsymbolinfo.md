---
title: IDebugModule3::GetSymbolInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd952242db8b7394fa8915319686ac431b84947d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323947"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
检索的符号，以及搜索每个路径的结果的搜索路径的列表。

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
[in]中的标志的组合[SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)枚举，它指定的哪些字段`pInfo`要填充的。

`pInfo`\
[out]一个[MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)其成员是否使用指定的信息填充的结构。 如果这是一个 null 值，此方法返回`E_INVALIDARG`。

## <a name="return-value"></a>返回值
如果此方法成功，它将返回`S_OK`; 否则为它将返回错误代码。

> [!NOTE]
> 返回的字符串 (在`MODULE_SYMBOL_SEARCH_INFO`结构) 可能是空即使`S_OK`返回。 在这种情况下，没有要返回的搜索信息。

## <a name="remarks"></a>备注
如果`bstrVerboseSearchInfo`字段的`MODULE_SYMBOL_SEARCH_INFO`结构不为空，则它包含搜索路径和该搜索的结果的列表。 列表格式与跟省略号 （"..."） 后, 跟结果的路径。 如果有多个路径结果对，然后由"\r\n"（回车符-/ 换行） 对分隔每个对。 该模式如下所示：

\<path>...\<result>\r\n\<path>...\<result>\r\n\<path>...\<result>

请注意，最后一项没有 \r\n 序列。

## <a name="example"></a>示例
在此示例中，此方法返回具有三个不同的搜索结果的三个路径。 每个行结尾的回车/换行符对。 示例输出只作为单个字符串输出搜索结果。

> [!NOTE]
> 所有内容的"..."在行结束之前，紧跟状态结果。

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

**c:\symbols\user32.pdb...找不到文件。** 
**c:\winnt\symbols\user32.pdb...版本不匹配。** 
 **\\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb...加载符号。**

## <a name="see-also"></a>请参阅

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
