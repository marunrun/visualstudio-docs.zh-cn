---
title: CA1053:静态容器类型不应具有构造函数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldNotHaveConstructors
- CA1053
helpviewer_keywords:
- CA1053
- StaticHolderTypesShouldNotHaveConstructors
ms.assetid: 10302b9a-fa5e-4935-a06a-513d9600f613
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44bdb8c12b48a983b88e6a035fc1522856b306be
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235589"
---
# <a name="ca1053-static-holder-types-should-not-have-default-constructors"></a>CA1053:静态容器类型不应具有默认构造函数

|||
|-|-|
|TypeName|StaticHolderTypesShouldNotHaveConstructors|
|CheckId|CA1053|
|类别|Microsoft.Design|
|重大更改|重大|

> [!NOTE]
> 规则 CA1053 合并为[CA1052：静态容器类型应在](ca1052-static-holder-types-should-be-sealed.md) [FxCop 分析器](fxcop-analyzers.yml)中密封。

## <a name="cause"></a>原因

公共或嵌套公共类型仅声明静态成员，并且具有默认构造函数。

## <a name="rule-description"></a>规则说明

默认构造函数是不必要的，因为调用静态成员不需要类型的实例。 另外，由于类型不具有非静态成员，因此创建实例时不提供对任何类型成员的访问。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除默认构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 如果存在默认的构造函数，则表明该类型不是静态类型。