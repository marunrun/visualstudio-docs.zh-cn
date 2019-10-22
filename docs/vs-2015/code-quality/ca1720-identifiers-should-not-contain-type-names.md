---
title: CA1720：标识符不应包含类型名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1720
- IdentifiersShouldNotContainTypeNames
helpviewer_keywords:
- IdentifiersShouldNotContainTypeNames
- CA1720
ms.assetid: c95ee48f-f23a-45f0-ac9e-a3c1ecfabdea
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 34ebe4848bbbe49b9a67449795f0aea7d104af8b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671630"
---
# <a name="ca1720-identifiers-should-not-contain-type-names"></a>CA1720：标识符不应包含类型名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldNotContainTypeNames|
|CheckId|CA1720|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见成员中参数的名称包含数据类型名称。

 或

 外部可见成员的名称包含特定于语言的数据类型名称。

## <a name="rule-description"></a>规则说明
 参数和成员的名称比描述其类型（需要由开发工具提供）更好。 对于成员的名称，如果必须使用数据类型名称，请使用与语言无关的名称，而不是特定于语言的名称。 例如，使用与语言无关C#的数据类型名称 Int32，而不是类型名称 "int"。

 将根据以下特定于语言的数据类型名称（不区分大小写）检查参数或成员名称中的每个离散标记：

- Bool

- WChar

- Int8

- UInt8

- Short

- UShort

- Int

- UInt

- 整数

- UInteger

- Long

- ULong

- 无符号

- 有符号

- Float

- Float32

- Float64

  此外，还会对照以下与语言无关的数据类型名称来检查参数的名称，但不区分大小写：

- 对象

- Obj

- 布尔值

- Char

- 字符串

- SByte

- 字节

- UByte

- Int16

- UInt16

- Int32

- UInt32

- Int64

- UInt64

- IntPtr

- Ptr

- 指针

- UInptr

- UPtr

- UPointer

- Single

- Double

- 十进制

- GUID

## <a name="how-to-fix-violations"></a>如何解决冲突
 **如果针对参数触发：**

 将参数名称中的数据类型标识符替换为可更好地描述其含义的字词或更通用的字词，如 "value"。

 **如果对成员触发：**

 将成员名称中特定于语言的数据类型标识符替换为可更好地描述其含义的术语、与语言无关的等效项或更通用的字词，如 "value"。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 偶尔使用基于类型的参数和成员名称可能是合适的。 但是，对于新的开发，不会出现任何已知方案，你应禁止显示此规则发出的警告。 对于先前随附的库，可能必须禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA1709：标识符的大小写应当正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708：标识符不应仅以大小写进行区分](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707：标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1719：参数名不应与成员名冲突](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)
