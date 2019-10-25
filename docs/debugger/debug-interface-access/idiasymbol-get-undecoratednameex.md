---
title: IDiaSymbol：： get_undecoratedNameEx |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedNameEx method
ms.assetid: 579aed0b-c57d-41a1-a94a-3bf665fd4a9d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 48efbc249d076853e12bc54d2e8a8d438570e740
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738997"
---
# <a name="idiasymbolget_undecoratednameex"></a>IDiaSymbol::get_undecoratedNameEx
检索C++修饰（链接）名称的部分或全部未经修饰的名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_undecoratedNameEx( 
   DWORD undecorateOptions,
   BSTR* pRetval
);
```

#### <a name="parameters"></a>参数
 `undecoratedOptions`

中指定用于控制返回内容的标志组合。 请参阅 "备注" 部分，了解具体的值以及它们的作用。

 `pRetVal`

弄返回C++修饰名的未修饰名。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 @No__t_0 可以是以下标志的组合。

> [!NOTE]
> DIA SDK 中未定义标志名称，因此需要将声明添加到代码中或使用原始值。

|Flag|“值”|描述|
|----------|-----------|-----------------|
|UNDNAME_COMPLETE|0x0000|启用完全 undecoration。|
|UNDNAME_NO_LEADING_UNDERSCORES|0x0001|删除 Microsoft 扩展关键字中的前导下划线。|
|UNDNAME_NO_MS_KEYWORDS|0x0002|禁止扩展 Microsoft 扩展关键字。|
|UNDNAME_NO_FUNCTION_RETURNS|0x0004|禁止对主声明的返回类型进行扩展。|
|UNDNAME_NO_ALLOCATION_MODEL|0x0008|禁止展开声明模型。|
|UNDNAME_NO_ALLOCATION_LANGUAGE|0x0010|禁用声明语言说明符的展开。|
|UNDNAME_RESERVED1|0x0020|已保留。|
|UNDNAME_RESERVED2|0x0040|已保留。|
|UNDNAME_NO_THISTYPE|0x0060|禁用 `this` 类型上的所有修饰符。|
|UNDNAME_NO_ACCESS_SPECIFIERS|0x0080|禁止扩展成员的访问说明符。|
|UNDNAME_NO_THROW_SIGNATURES|0x0100|禁止对函数和指向函数的指针展开 "throw 签名"。|
|UNDNAME_NO_MEMBER_TYPE|0x0200|禁用 `static` 或 `virtual` 成员的展开。|
|UNDNAME_NO_RETURN_UDT_MODEL|0x0400|禁止为 UDT 返回 Microsoft 模型的扩展。|
|UNDNAME_32_BIT_DECODE|0x0800|Undecorates 32 位修饰名。|
|UNDNAME_NAME_ONLY|0x1000|仅获取主声明的名称;仅返回 [scope：：] name。  展开模板参数。|
|UNDNAME_TYPE_ONLY|0x2000|输入只是一种类型编码;撰写抽象声明符。|
|UNDNAME_HAVE_PARAMETERS|0x4000|实际模板参数可用。|
|UNDNAME_NO_ECSU|0x8000|禁止枚举/类/结构/联合。|
|UNDNAME_NO_IDENT_CHAR_CHECK|0x10000|禁止检查有效的标识符字符。|
|UNDNAME_NO_PTR64|0x20000|不在输出中包括 ptr64。|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)