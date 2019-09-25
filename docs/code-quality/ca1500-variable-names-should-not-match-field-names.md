---
title: CA1500:变量名不应与字段名相同
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
helpviewer_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
ms.assetid: fa0e5029-79e9-4a33-8576-787ac3c26c39
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: fbc3fbeac6d01b718af2022a09bddb92e9c7c2c6
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234575"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500:变量名不应与字段名相同

|||
|-|-|
|TypeName|VariableNamesShouldNotMatchFieldNames|
|CheckId|CA1500|
|类别|Microsoft.Maintainability|
|重大更改|对与字段具有相同名称的参数触发时：<br /><br /> -"不间断"-如果在程序集外部不显示声明参数的字段和方法，无论所做的更改如何。<br />-中断-如果更改字段的名称，则可以在程序集外部查看。<br />-如果您更改参数的名称，则可以在程序集外部查看该参数的名称。<br /><br /> 当在与字段同名的局部变量上触发时：<br /><br /> -"不间断"-如果在程序集外部不能查看该字段，无论你进行了何种更改。<br />-"非换行"-如果更改本地变量的名称，并且不更改字段的名称，则为。<br />-如果更改字段的名称，则可以在程序集外部查看。|

## <a name="cause"></a>原因

实例方法声明的参数或本地变量的名称与声明类型的实例字段匹配。 若要捕获违反规则的局部变量，则必须使用调试信息来生成经过测试的程序集，并且关联的程序数据库（.pdb）文件必须可用。

## <a name="rule-description"></a>规则说明

当实例字段的名称与参数或局部变量名称匹配时，将在方法体中使用`this` （`Me` in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]）关键字来访问实例字段。 维护代码时，很容易忘记这种差异，并假设参数/局部变量引用实例字段，这将导致错误。 这适用于较长的方法体。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请重命名参数/变量或字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例显示了两个规则冲突。

[!code-vb[FxCop.Maintainability.VarMatchesField#1](../code-quality/codesnippet/VisualBasic/ca1500-variable-names-should-not-match-field-names_1.vb)]
[!code-csharp[FxCop.Maintainability.VarMatchesField#1](../code-quality/codesnippet/CSharp/ca1500-variable-names-should-not-match-field-names_1.cs)]