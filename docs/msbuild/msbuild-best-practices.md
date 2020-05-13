---
title: MSBuild 最佳做法 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91b2e157ee64f5e4d91bc75a5d6f8d65d4312862
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "78263144"
---
# <a name="msbuild-best-practices"></a>MSBuild 最佳做法

我们建议下列编写 MSBuild 脚本的最佳做法：

- 默认属性值的最佳处理方式是使用 `Condition` 特性，而不是声明可在命令行中重写其默认值的属性。 例如，使用

```xml
<MyProperty Condition="'$(MyProperty)' == ''">
   MyDefaultValue
</MyProperty>
```

- 通常，选择项时，请避免使用通配符。 而应显式指定文件。 这是因为在大多数项目类型中，MSBuild 会在不同时间展开通配符，如添加或删除项时，这可能会导致意外行为。 在 .NET Core SDK 样式项目中有一个例外，该项目可以正确处理通配符。

## <a name="see-also"></a>请参阅

- [高级概念](../msbuild/msbuild-advanced-concepts.md)
