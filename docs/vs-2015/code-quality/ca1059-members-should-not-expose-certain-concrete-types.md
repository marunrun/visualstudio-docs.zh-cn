---
title: CA1059:成员不应公开某些具体类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1059
- MembersShouldNotExposeCertainConcreteTypes
helpviewer_keywords:
- MembersShouldNotExposeCertainConcreteTypes
- CA1059
ms.assetid: 59f61f52-8d6c-49cb-aefb-191910523a3c
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a78125645dc6369811b4b9e1d7101b7bb4cbba76
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200494"
---
# <a name="ca1059-members-should-not-expose-certain-concrete-types"></a>CA1059:成员不应公开某些具体类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MembersShouldNotExposeCertainConcreteTypes|
|CheckId|CA1059|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见成员是某些具体类型或公开某些具体类型通过其参数之一或返回值。 目前，此规则将报告以下具体类型的风险：

- 一个类型派生自<xref:System.Xml.XmlNode?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 具体类型是指具有一个完整实现因此可以实例化的类型。 若要允许的成员被广泛使用，将使用建议的接口为具体类型。 这样，要接受实现该接口的任何类型或实现该接口的类型的地方使用的成员。

 下表列出了具体的目标的类型和它们的建议替换项。

|具体类型|Replacement|
|-------------------|-----------------|
|<xref:System.Xml.XPath.XPathDocument>|<xref:System.Xml.XPath.IXPathNavigable?displayProperty=fullName>。<br /><br /> 使用该接口将分离中 XML 数据源的特定实现的成员。|

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，更改为建议的接口的具体类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它是安全地禁止显示此规则从一条消息，如果提供的具体类型的特定功能是必需的。

## <a name="related-rules"></a>相关的规则
 [CA1011:请考虑将基类型作为参数传递](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)
