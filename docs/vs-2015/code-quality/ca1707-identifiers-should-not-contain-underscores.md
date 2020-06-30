---
title: CA1707：标识符不应包含下划线 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotContainUnderscores
- CA1707
helpviewer_keywords:
- CA1707
- IdentifiersShouldNotContainUnderscores
ms.assetid: 5fb539ef-c304-4323-90c0-b14386da9774
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fe6b90ef971bd00392381f47860d85f34e10dc26
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544022"
---
# <a name="ca1707-identifiers-should-not-contain-underscores"></a>CA1707:标识符不应包含下划线
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[CA1707：标识符不应包含下划线](/visualstudio/code-quality/ca1707-identifiers-should-not-contain-underscores)。

|Item|值|
|-|-|
|TypeName|IdentifiersShouldNotContainUnderscores|
|CheckId|CA1707|
|Category|Microsoft。命名|
|是否重大更改|正在进行-对程序集引发<br /><br /> 无间断-在类型参数上引发|

## <a name="cause"></a>原因
 标识符的名称包含下划线（_）字符。

## <a name="rule-description"></a>规则描述
 按照约定，标识符名称不包含下划线 (_) 字符。 规则将检查命名空间、类型、成员和参数。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 删除名称中的所有下划线字符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA1709:标识符的大小写应当正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:标识符应以大小写之外的差别进行区分](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
