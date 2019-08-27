---
title: CA1501:避免过度继承
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1501
- AvoidExcessiveInheritance
helpviewer_keywords:
- AvoidExcessiveInheritance
- CA1501
ms.assetid: 9e934746-1a4d-492a-91e4-085201abafa4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d77ecc255f03e38e39a9321d9c7a9e5568e94a4d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546331"
---
# <a name="ca1501-avoid-excessive-inheritance"></a>CA1501:避免过度继承

|||
|-|-|
|TypeName|AvoidExcessiveInheritance|
|CheckId|CA1501|
|类别|Microsoft.Maintainability|
|是否重大更改|重大|

## <a name="cause"></a>原因

类型在继承层次结构中的深度超过四级。

## <a name="rule-description"></a>规则说明

深度嵌套的类型层次结构可能很难遵循、理解和维护。 此规则将分析限制的同一模块中的层次结构。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请从继承层次结构中较浅的基类型派生类型或消除一些中间的基类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告。 但是，代码可能更难以维护。 请注意，具体取决于基类型的可见性，解决此规则冲突的情况可能会造成重大更改。 例如，删除公共基类型是一项重大更改。

## <a name="example"></a>示例

下面的示例所示违反了此规则的类型：

[!code-csharp[FxCop.Maintainability.ExcessiveInheritance#1](../code-quality/codesnippet/CSharp/ca1501-avoid-excessive-inheritance_1.cs)]
[!code-vb[FxCop.Maintainability.ExcessiveInheritance#1](../code-quality/codesnippet/VisualBasic/ca1501-avoid-excessive-inheritance_1.vb)]