---
title: IDebugProperty3：： GetStringChars |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetStringChars
helpviewer_keywords:
- IDebugProperty3::GetStringChars
ms.assetid: 832c37f3-85cb-4227-8ab2-f27a80eafe90
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 693a29bc30ef206428713ace36275389de1b7f0a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721080"
---
# <a name="idebugproperty3getstringchars"></a>IDebugProperty3::GetStringChars
检索与此属性关联的字符串，并将其存储在用户提供的缓冲区中。

## <a name="syntax"></a>语法

```cpp
HRESULT GetStringChars(
    ULONG  buflen,
    WCHAR* rgString,
    ULONG* pceltFetched
);
```

```csharp
int GetStringChars(
    uint       buflen,
    out string rgString,
    out uint   pceltFetched
);
```

## <a name="parameters"></a>参数
`buflen`\
中用户提供的缓冲区可以容纳的最大字符数。

`rgString`\
弄返回字符串。

 [仅限 c + +] `rgString` 是指向接收字符串的 Unicode 字符的缓冲区的指针。 此缓冲区必须至少为 `buflen` 个字符， (大小不能) 字节。

`pceltFetched`\
弄返回缓冲区中实际存储的字符数。  (可以是 `NULL` c + + 中的 ) 

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
在 c + + 中，必须小心确保缓冲区的长度至少为 `buflen` Unicode 字符。 请注意，Unicode 字符的长度为2个字节。

> [!NOTE]
> 在 c + + 中，返回的字符串不包含终止 null 字符。 如果给定， `pceltFetched` 将指定字符串中的字符数。

## <a name="example"></a>示例

```cpp
CStringW RetrievePropertyString(IDebugProperty2 *pPropInfo)
{
    CStringW returnString = L"";
    CComQIPtr<IDebugProperty3> pProp3 = pPropInfo->pProperty;
    If (pProp3 != NULL) {
        ULONG dwStrLen = 0;
        HRESULT hr;
        hr = pProp3->GetStringCharLength(&dwStrLen);
        if (SUCCEEDED(hr) && dwStrLen > 0) {
            ULONG dwRead;
            CStrBufW buf(returnString,dwStrLen,CStrBuf::SET_LENGTH);
            hr = pProp3->GetStringChars(dwStrLen,
                                        reinterpret_cast<WCHAR*>(static_cast<CStringW::PXSTR>(buf)),
                                        &dwRead);
        }
    }
    return(returnString);
}
```

## <a name="see-also"></a>另请参阅
- [GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
