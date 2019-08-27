---
title: CA1051:不要声明可见实例字段
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1051
- DoNotDeclareVisibleInstanceFields
helpviewer_keywords:
- CA1051
- DoNotDeclareVisibleInstanceFields
ms.assetid: 2805376c-824c-462c-81d1-c51aaf7cabe7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5dd8a4b2d0b32a8c52f75dee6fd765a7ea6ec9a
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547557"
---
# <a name="ca1051-do-not-declare-visible-instance-fields"></a>CA1051:不要声明可见实例字段

|||
|-|-|
|TypeName|DoNotDeclareVisibleInstanceFields|
|CheckId|CA1051|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因

类型具有非私有实例字段。

默认情况下, 此规则仅查看外部可见类型, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

字段的主要用途应是作为实现的详细信息。 字段应为`private`或`internal`并且应使用属性公开。 在访问某个字段时, 可以轻松访问该属性, 而属性访问器中的代码可以在扩展类型功能时更改, 而不会引入重大更改。 仅返回私有字段或内部字段的值的属性, 经过优化, 可在与访问字段相同的情况上执行:性能提升极少与属性上的外部可见字段的使用相关联。

外部可见是指`public`、 `protected`和`protected internal` (`Public`、 `Protected`和inVisualBasic)可访问性级别。`Protected Friend`

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突, 请将`private`该`internal`字段设置为, 并使用外部可见的属性将其公开。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 外部可见字段不提供属性无法使用的任何权益。 此外, 公共字段不能通过[链接要求](/dotnet/framework/misc/link-demands)进行保护。 请[参阅 CA2112:受保护的类型不应](../code-quality/ca2112-secured-types-should-not-expose-fields.md)公开字段。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1051.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (设计) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的示例演示违反此规则`BadPublicInstanceFields`的类型 ()。 `GoodPublicInstanceFields`显示更正后的代码。

[!code-csharp[FxCop.Design.TypesPublicInstanceFields#1](../code-quality/codesnippet/CSharp/ca1051-do-not-declare-visible-instance-fields_1.cs)]

## <a name="related-rules"></a>相关规则

- [CA2112受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

## <a name="see-also"></a>请参阅

- [链接需求](/dotnet/framework/misc/link-demands)