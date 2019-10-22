---
title: CA1053：静态容器类型不应具有构造函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldNotHaveConstructors
- CA1053
helpviewer_keywords:
- CA1053
- StaticHolderTypesShouldNotHaveConstructors
ms.assetid: 10302b9a-fa5e-4935-a06a-513d9600f613
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7de098d264dbdd6d7d9daea385de2e03d4e1ba35
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653825"
---
# <a name="ca1053-static-holder-types-should-not-have-constructors"></a>CA1053：静态容器类型不应具有构造函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|StaticHolderTypesShouldNotHaveConstructors|
|CheckId|CA1053|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或嵌套公共类型只声明了静态成员，但具有公共或受保护的默认构造函数。

## <a name="rule-description"></a>规则说明
 由于调用静态成员不需要类型的示例，因此没必要使用构造函数。 另外，由于类型不具有非静态成员，因此创建实例时不提供对任何类型成员的访问。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除默认构造函数或将其设置为私有。

> [!NOTE]
> 如果类型没有定义任何构造函数，某些编译器会自动创建公共默认构造函数。 如果您的类型是这种情况，则添加私有默认构造函数以消除冲突。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 如果存在构造函数，则表明该类型不是静态类型。

## <a name="example"></a>示例
 下面的示例演示违反此规则的类型。 请注意，源代码中没有默认的构造函数。 将此代码编译为程序集时， C#编译器将插入默认构造函数，这将违反此规则。 若要更正此错误，请声明一个私有构造函数。

 [!code-csharp[FxCop.Design.StaticTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.StaticTypes/cs/FxCop.Design.StaticTypes.cs#1)]
