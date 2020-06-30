---
title: CA1500：变量名不应与字段名称匹配 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
helpviewer_keywords:
- VariableNamesShouldNotMatchFieldNames
- CA1500
ms.assetid: fa0e5029-79e9-4a33-8576-787ac3c26c39
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9565bc1ae3166c0475e8af7f0fde381497309b01
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547909"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500:变量名不应与字段名相同
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[CA1500：变量名不应与字段名称匹配](/visualstudio/code-quality/ca1500-variable-names-should-not-match-field-names)。

|Item|值|
|-|-|
|TypeName|VariableNamesShouldNotMatchFieldNames|
|CheckId|CA1500|
|Category|Microsoft 可维护性|
|是否重大更改|对与字段具有相同名称的参数触发时：<br /><br /> -"不间断"-如果在程序集外部不显示声明参数的字段和方法，无论所做的更改如何。<br />-中断-如果更改字段的名称，则可以在程序集外部查看。<br />-如果您更改参数的名称，则可以在程序集外部查看该参数的名称。<br /><br /> 当在与字段同名的局部变量上触发时：<br /><br /> -"不间断"-如果在程序集外部不能查看该字段，无论你进行了何种更改。<br />-"非换行"-如果更改本地变量的名称，并且不更改字段的名称，则为。<br />-如果更改字段的名称，则可以在程序集外部查看。|

## <a name="cause"></a>原因
 实例方法声明的参数或本地变量的名称与声明类型的实例字段匹配。 若要捕获违反规则的局部变量，则必须使用调试信息来生成经过测试的程序集，并且关联的程序数据库（.pdb）文件必须可用。

## <a name="rule-description"></a>规则描述
 当实例字段的名称与参数或局部变量名称匹配时，将在 `this` `Me` 方法体中使用（in）关键字来访问实例字段 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 。 维护代码时，很容易忘记这种差异，并假设参数/局部变量引用实例字段，这将导致错误。 这适用于较长的方法体。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请重命名参数/变量或字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了两个规则冲突。

 [!code-csharp[FxCop.Maintainability.VarMatchesField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/cs/FxCop.Maintainability.VarMatchesField.cs#1)]
 [!code-vb[FxCop.Maintainability.VarMatchesField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/vb/FxCop.Maintainability.VarMatchesField.vb#1)]
