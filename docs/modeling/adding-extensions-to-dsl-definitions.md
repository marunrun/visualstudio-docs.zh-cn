---
title: 向 DSL 定义中添加扩展
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa5c02fc28e7ffec4765d94758c838ab149e7ac3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62960480"
---
# <a name="add-extensions-to-dsl-definitions"></a>向 DSL 定义中添加扩展

DSL 定义扩展插件，可创建的域特定语言 (DSL) 的扩展包。 DSL 的方式相同，DSL 扩展，它包含在 Visual Studio 集成扩展 (VSIX) 中，可以安装在用户的计算机上。 可以动态启用和禁用在运行时的其他功能。 Dsl 无需显式设计为扩展插件，并扩展可以被设计为更高版本，或者由第三方，而无需更改扩展的 DSL。

DSL 扩展可以包括以下功能：

- 模型和表示元素的属性

- 形状和连接符的修饰器

- 类、 关系、 形状和连接器

- 验证约束

- 工具箱项和选项卡

扩展 DSL 的用户可以创建和保存模型，其中包含其他功能的实例。 已安装相应的扩展的其他用户可以读取模型。 未安装该扩展的用户不能使用其他功能，但它们可以更新和保存模型而不会丢失的其他功能。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
