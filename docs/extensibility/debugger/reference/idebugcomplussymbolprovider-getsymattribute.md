---
title: IDebugComPlus符号提供程序：：获取Sym属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetSymAttribute
- GetSymAttribute
ms.assetid: 6cbaac92-a60b-4165-a7f5-c34407770f3c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cb405bd0cf6f3ec846e3b146e4fd02399d583fb7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733771"
---
# <a name="idebugcomplussymbolprovidergetsymattribute"></a>IDebugComPlusSymbolProvider::GetSymAttribute
使用指定模块的给定父属性检索调试符号。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymAttribute (
    ULONG32  ulAppDomainID,
    GUID     guidModule,
    _mdToken tokParent,
    LPOLESTR pstrName,
    ULONG32  cBuffer,
    ULONG32* pcBuffer,
    BYTE*    buffer
);
```

```csharp
int GetSymAttribute (
    uint      ulAppDomainID,
    Guid      guidModule,
    int       tokParent,
    string    pstrName,
    uint      cBuffer,
    out uint  pcBuffer,
    out int[] buffer
);
```

## <a name="parameters"></a>参数
`ulAppDomainID`\
[在]应用程序域的标识符。

`guidModule`\
[在]模块的唯一标识符。

`tokParent`\
[在]父属性的令牌。

`pstrName`\
[在]模块的名称。

`cBuffer`\
[在]输出`buffer`所需的字节数。

`pcBuffer`\
[出]输出`buffer`的长度。

`buffer`\
[出]包含符号的数组。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugComPlusSymbol提供程序](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的**CDebugSymbol提供程序**对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::GetSymAttribute(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    _mdToken tokParent,
    __in_z LPOLESTR pstrName,
    ULONG32 cBuffer,
    ULONG32 *pcBuffer,
    BYTE buffer[])
{
    HRESULT hr = S_OK;
    CComPtr<CModule> pModule;
    Module_ID idModule(ulAppDomainID, guidModule);

    METHOD_ENTRY( CDebugSymbolProvider::GetSymAttribute );

    IfFailGo( GetModule( idModule, &pModule) );

    IfFailGo( pModule->GetSymAttribute( tokParent, pstrName, cBuffer, pcBuffer, buffer ) );

Error:

    METHOD_EXIT(CDebugSymbolProvider::GetSymAttribute, hr);

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
