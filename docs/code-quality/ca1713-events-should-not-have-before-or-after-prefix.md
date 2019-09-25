---
title: CA1713:事件不应具有 before 或 after 前缀
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EventsShouldNotHaveBeforeOrAfterPrefix
- CA1713
helpviewer_keywords:
- CA1713
- EventsShouldNotHaveBeforeOrAfterPrefix
ms.assetid: 855772a4-aa9e-410b-88c1-c5fba1ca63da
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 834c0f73a1fdc26f06c62e1c6e3a2d19372a244d
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234102"
---
# <a name="ca1713-events-should-not-have-before-or-after-prefix"></a>CA1713:事件不应具有 before 或 after 前缀

|||
|-|-|
|TypeName|EventsShouldNotHaveBeforeOrAfterPrefix|
|CheckId|CA1713|
|类别|Microsoft.Naming|
|重大更改|重大|

## <a name="cause"></a>原因
事件的名称以 "Before" 或 "After" 开头。

## <a name="rule-description"></a>规则说明
事件名称应描述引发事件的操作。 若要命名按特定顺序引发的相关事件，请使用现在时或过去时指示一系列操作中的相对位置。 例如，在为关闭资源时引发的事件对进行命名时，可以将其命名为 "关闭" 和 "关闭"，而不是 "BeforeClose" 和 "AfterClose"。

命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突
从事件名称中删除前缀，并考虑将该名称更改为使用谓词的现在时或过去时。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。