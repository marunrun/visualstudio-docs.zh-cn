---
title: CA2237：用 SerializableAttribute 标记 ISerializable 类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2237
- MarkISerializableTypesWithSerializable
helpviewer_keywords:
- MarkISerializableTypesWithSerializable
- CA2237
ms.assetid: 9bd6bb24-a527-43dd-9952-043c0c694f46
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c548eb76ba36099d0cef5b651a095f35d64e033c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666696"
---
# <a name="ca2237-mark-iserializable-types-with-serializableattribute"></a>CA2237：以 SerializableAttribute 标记 ISerializable 类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkISerializableTypesWithSerializable|
|CheckId|CA2237|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 外部可见类型实现 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 接口，并且该类型未使用 <xref:System.SerializableAttribute?displayProperty=fullName> 特性进行标记。 规则将忽略基类型无法序列化的派生类型。

## <a name="rule-description"></a>规则说明
 要由公共语言运行时识别为可序列化，即使类型通过实现 <xref:System.Runtime.Serialization.ISerializable> 接口使用自定义序列化例程，也必须使用 <xref:System.SerializableAttribute> 特性标记类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 <xref:System.SerializableAttribute> 属性应用于该类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则中的异常类的警告，因为它们必须是可序列化的，才能在应用程序域间正常工作。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。 取消注释 <xref:System.SerializableAttribute> 特性行来满足规则。

 [!code-csharp[FxCop.Usage.MarkSerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/cs/FxCop.Usage.MarkSerializable.cs#1)]
 [!code-vb[FxCop.Usage.MarkSerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/vb/FxCop.Usage.MarkSerializable.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2236：对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240：正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238：正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2239：为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120：保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
