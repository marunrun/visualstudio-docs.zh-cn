---
title: CA1500:变量名不应与字段名称 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8dc15c95398ed45954c3830d1c558a6653a4346f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191490"
---
# <a name="ca1500-variable-names-should-not-match-field-names"></a>CA1500:变量名不应与字段名相同
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[CA1500:变量名不应与字段名](https://docs.microsoft.com/visualstudio/code-quality/ca1500-variable-names-should-not-match-field-names)。  
  
|||  
|-|-|  
|TypeName|VariableNamesShouldNotMatchFieldNames|  
|CheckId|CA1500|  
|类别|Microsoft.Maintainability|  
|是否重大更改|当触发对与字段具有相同名称的参数：<br /><br /> --否-如果外的程序集，而不考虑所做的更改都不可见的字段和方法，它将参数声明。<br />-是-如果更改字段的名称和程序集外可见。<br />-是参数的-如果您更改名称和程序集外可见声明它的方法。<br /><br /> 如果在与字段具有相同名称的本地变量上引发：<br /><br /> --否-如果该字段不能看到外部程序集，而不考虑所做的更改。<br />--否-如果更改本地变量的名称，而不更改的字段的名称。<br />-是-如果您更改字段的名称并且可将它视为程序集外部的。|  
  
## <a name="cause"></a>原因  
 实例方法声明的参数或局部变量的名称匹配的声明类型的实例字段。 若要捕获与规则冲突的本地变量，测试的程序集必须使用调试信息来生成和关联的程序数据库 (.pdb) 文件必须可用。  
  
## <a name="rule-description"></a>规则说明  
 当某一实例字段的名称匹配的参数或局部变量的名称时，使用访问实例字段`this`(`Me`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 的方法主体内的关键字。 当维护代码，很容易忘记了这种差异，假定参数/本地变量引用实例字段，这将导致错误。 这是特别是对于较长的方法正文，则返回 true。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 若要修复此规则的冲突，请重命名参数/变量或字段。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 不禁止显示此规则发出的警告。  
  
## <a name="example"></a>示例  
 下面的示例演示两个规则的冲突。  
  
 [!code-csharp[FxCop.Maintainability.VarMatchesField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/cs/FxCop.Maintainability.VarMatchesField.cs#1)]
 [!code-vb[FxCop.Maintainability.VarMatchesField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.VarMatchesField/vb/FxCop.Maintainability.VarMatchesField.vb#1)]
