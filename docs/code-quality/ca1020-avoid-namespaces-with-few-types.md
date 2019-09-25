---
title: CA1020:避免使用类型极少的命名空间
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1020
- AvoidNamespacesWithFewTypes
helpviewer_keywords:
- CA1020
- AvoidNamespacesWithFewTypes
ms.assetid: 9cb272f6-a3ff-45af-b35d-70dea620b074
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6e5c50f607253304b05dd7ab9350646a0df05e70
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236228"
---
# <a name="ca1020-avoid-namespaces-with-few-types"></a>CA1020:避免使用类型极少的命名空间

|||
|-|-|
|TypeName|AvoidNamespacesWithFewTypes|
|CheckId|CA1020|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因

除全局命名空间之外的命名空间包含的类型少于五个。

## <a name="rule-description"></a>规则说明

请确保每个命名空间都有一个逻辑组织，并确保将类型放入稀疏填充的命名空间中的原因是有效的。 命名空间应包含在大多数情况下一起使用的类型。 当它们的应用程序互斥时，类型应位于单独的命名空间中。 例如， <xref:System.Web.UI>命名空间包含在 web 应用程序中使用的类型， <xref:System.Windows.Forms>命名空间包含在基于的应用程序中[!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)]使用的类型。 即使两个命名空间都具有控制用户界面各方面的类型，这些类型也并不是旨在用于同一应用程序。 因此，它们位于单独的命名空间中。 小心命名空间组织也有帮助，因为这样可以提高功能的可发现性。 通过检查命名空间层次结构，库使用者应该能够找到实现功能的类型。

> [!NOTE]
> 不应将设计时类型和权限合并到其他命名空间，以符合此准则。 这些类型在您的主命名空间下面的命名空间中，并且命名空间应`.Design`分别`.Permissions`以和结束。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请尝试将只包含几种类型的命名空间合并为单个命名空间。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果命名空间不包含与其他命名空间中的类型一起使用的类型，则可以安全地禁止显示此规则发出的警告。