---
title: CA1804:删除未使用的局部变量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1804
- RemoveUnusedLocals
helpviewer_keywords:
- RemoveUnusedLocals
- CA1804
ms.assetid: cc332e67-6543-4813-bd8a-6f6fc75bf22a
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 38fe76bbdf2fdafa69ca12caf4f131a05f783954
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143120"
---
# <a name="ca1804-remove-unused-locals"></a>CA1804:移除未使用的局部变量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|RemoveUnusedLocals|
|CheckId|CA1804|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 方法声明本地变量，但不使用除变量可能是作为接收方的赋值语句。 有关此规则分析，必须使用调试信息生成测试的程序集和关联的程序数据库 (.pdb) 文件必须可用。

## <a name="rule-description"></a>规则说明
 未使用的局部变量和不必要的赋值会增加程序集的大小并降低性能。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除或使用本地变量。 请注意，C# 编译器的是附带[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]删除未使用的本地变量时`optimize`选项处于启用状态。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果变量是编译器发出，禁止显示此规则的警告。 如果性能和代码维护不关注的主要问题，则也可以禁止显示此规则的警告或禁用规则，安全。

## <a name="example"></a>示例
 下面的示例显示了多个未使用的本地变量。

 [!code-csharp[FxCop.Performance.UnusedLocals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnusedLocals/cs/FxCop.Performance.UnusedLocals.cs#1)]
 [!code-vb[FxCop.Performance.UnusedLocals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UnusedLocals/vb/FxCop.Performance.UnusedLocals.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1809:避免过多的局部变量](../code-quality/ca1809-avoid-excessive-locals.md)

 [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1812:避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801:检查未使用的参数](../code-quality/ca1801-review-unused-parameters.md)
