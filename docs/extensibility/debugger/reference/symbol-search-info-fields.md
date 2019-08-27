---
title: SYMBOL_SEARCH_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SYMBOL_SEARCH_INFO_FIELDS
helpviewer_keywords:
- SYMBOL_SEARCH_INFO_FIELDS enumeration
ms.assetid: bce35af0-722d-46d4-afa6-eaae598c51ff
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86a7fb7c891d0c22bc415920014e905cf3d9c6fa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322367"
---
# <a name="symbolsearchinfofields"></a>SYMBOL_SEARCH_INFO_FIELDS
指定要检索的符号信息的类型。

## <a name="syntax"></a>语法

```cpp
enum enum_SYMBOL_SEARCH_INFO_FIELDS
{
   SSIF_NONE                = 0x00000000,
   SSIF_VERBOSE_SEARCH_INFO = 0x00000001
};
typedef DWORD SYMBOL_SEARCH_INFO_FIELDS;
```

```csharp
public enum enum_SYMBOL_SEARCH_INFO_FIELDS
{
   SSIF_NONE                = 0x00000000,
   SSIF_VERBOSE_SEARCH_INFO = 0x00000001
};

```

## <a name="fields"></a>字段
 `SSIF_NONE`\
 不指示任何标志

 `SSIF_VERBOSE_SEARCH_INFO`\
 返回所有搜索路径用于查找符号

## <a name="remarks"></a>备注
 这些标志作为参数传递给[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)方法来确定的少量信息返回。

> [!NOTE]
> 目前，仅`SSIF_VERBOSE_SEARCH_INFO`受支持，且它必须指定为`dwFlags`参数`IDebugModule3::GetSymbolInfo`。 所有其他值返回错误。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)