---
title: 向 DSL 定义中添加扩展
description: 了解 DSL 定义扩展如何允许你为特定于域的语言 (DSL) 创建扩展包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 07057c24494a19d77bca872ad87adf20bb125252
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2020
ms.locfileid: "97361139"
---
# <a name="add-extensions-to-dsl-definitions"></a>向 DSL 定义中添加扩展

DSL 定义扩展允许你创建一个扩展包，将其扩展到域特定语言 (DSL) 。 可采用与 DSL 相同的方式在用户计算机上安装 DSL 扩展，该扩展包含在 Visual Studio 集成扩展 (VSIX) 中。 在运行时可以动态启用和禁用其他功能。 Dsl 无需显式设计用于扩展，并且可以在以后或第三方设计扩展，而无需更改扩展 DSL。

DSL 扩展可以包含以下功能：

- 模型和表示元素的属性

- 形状和连接线的修饰器

- 类、关系、形状和连接线

- 验证约束

- 工具箱项和选项卡

扩展 DSL 的用户可以创建和保存包含附加功能实例的模型。 已安装适当扩展的其他用户可以读取该模型。 尚未安装此扩展的用户不能使用其他功能，但可以更新和保存模型，而不会丢失其他功能。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
