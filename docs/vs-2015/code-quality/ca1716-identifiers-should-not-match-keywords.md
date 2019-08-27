---
title: CA1716:标识符不应与关键字 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
helpviewer_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
ms.assetid: 900cc8a1-1089-4069-a4ce-10b109ac4fab
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 35a97e62e17895cb700a1420c7851878f329112a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189110"
---
# <a name="ca1716-identifiers-should-not-match-keywords"></a>CA1716:标识符不应与关键字冲突
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldNotMatchKeywords|
|CheckId|CA1716|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
 命名空间、 类型或虚拟或接口成员的名称匹配的编程语言中的保留的关键字。

## <a name="rule-description"></a>规则说明
 命名空间、 类型、 标识符和虚拟和接口成员不应与面向公共语言运行时的语言所定义的关键字。 根据使用的语言和关键字，编译器错误和二义性可以使库难以使用。

 此规则检查针对以下语言中的关键字：

- Visual Basic

- C#

- C++/CLI

  有关使用不区分大小写比较[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]用于其他语言的关键字，并区分大小写比较。

## <a name="how-to-fix-violations"></a>如何解决冲突
 关键字的列表中选择不会出现的名称。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果您确信标识符将混淆的 API，用户和库是所有可用语言中可用，可以禁止显示此规则的警告[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。
