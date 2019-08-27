---
title: CA2226:运算符应有对称重载
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
helpviewer_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
ms.assetid: d202401a-ea14-4559-b15e-0ea4f5b68789
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4557b61afab08c7db05c734c6f2ac927a40edb71
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546854"
---
# <a name="ca2226-operators-should-have-symmetrical-overloads"></a>CA2226:运算符应有对称重载

|||
|-|-|
|TypeName|OperatorsShouldHaveSymmetricalOverloads|
|CheckId|CA2226|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

某个类型实现了相等运算符或不等运算符，却未实现相反运算符。

默认情况下, 此规则仅查看外部可见类型, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

在某些情况下, 相等性或不等性适用于类型的实例, 而相反的运算符未定义。 类型通常通过返回相等运算符的求反值来实现不相等运算符。

对于C#违反此规则的情况, 编译器将发出错误。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突, 请同时实现相等运算符和不相等运算符, 或删除存在的运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 如果这样做, 您的类型将无法以与 .NET 一致的方式工作。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca2226.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (使用情况) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="related-rules"></a>相关规则

- [CA1046不要对引用类型重载运算符 equals](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)
- [CA2225运算符重载具有命名的备用项](../code-quality/ca2225-operator-overloads-have-named-alternates.md)
- [CA2224重载运算符等于时重写 equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)
- [CA2218重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)
- [CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)