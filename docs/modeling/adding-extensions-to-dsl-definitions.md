---
title: 向 DSL 定义中添加扩展
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f3e44c79783479c46247e4026788725d6ae16da7
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747653"
---
# <a name="add-extensions-to-dsl-definitions"></a>向 DSL 定义中添加扩展

DSL 定义扩展允许你创建一包扩展到域特定语言（DSL）的扩展。 在 Visual Studio 集成扩展（VSIX）中包含的 DSL 扩展可以与 DSL 相同的方式安装在用户的计算机上。 在运行时可以动态启用和禁用其他功能。 Dsl 无需显式设计用于扩展，并且可以在以后或第三方设计扩展，而无需更改扩展 DSL。

DSL 扩展可以包含以下功能：

- 模型和表示元素的属性

- 形状和连接线的修饰器

- 类、关系、形状和连接线

- 验证约束

- 工具箱项和选项卡

扩展 DSL 的用户可以创建和保存包含附加功能实例的模型。 已安装适当扩展的其他用户可以读取该模型。 尚未安装此扩展的用户不能使用其他功能，但可以更新和保存模型，而不会丢失其他功能。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>请参阅

- [相关博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
