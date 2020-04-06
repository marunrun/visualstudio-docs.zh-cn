---
title: IDebug属性3：：获取字符串字符 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
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
[在]用户提供的缓冲区可以保留的最大字符数。

`rgString`\
[出]返回字符串。

 [C++仅`rgString`]，是指向接收字符串 Unicode 字符的缓冲区的指针。 此缓冲区的大小必须至少`buflen`为字符（而不是字节）。

`pceltFetched`\
[出]返回缓冲区中实际存储的字符数。 （可在`NULL`C++。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则返回错误代码。

## <a name="remarks"></a>备注
在C++时，必须注意确保缓冲区至少`buflen`为 Unicode 字符长。 请注意，Unicode 字符长 2 字节。

> [!NOTE]
> 在C++，返回的字符串不包括终止空字符。 如果给定，`pceltFetched`将指定字符串中的字符数。

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

## <a name="see-also"></a>请参阅
- [GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
