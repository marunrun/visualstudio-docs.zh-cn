---
title: Visual Studio 的建模 SDK - 特定于域的语言
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools
- Domain-Specific Language
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e9e58de3737acaae01939eb2e29242e02888235d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658399"
---
# <a name="modeling-sdk-for-visual-studio---domain-specific-languages"></a>Visual Studio 的建模 SDK - 特定于域的语言

通过使用 Visual Studio 的建模 SDK，你可以创建可集成到 Visual Studio 中的功能强大的基于模型的开发工具。 同样，你可以创建一个或多个模型定义并将其集成到工具集中。

MSDK 的核心是你创建的用于表示业务领域内概念的模型的定义。 您可以使用各种工具来包围模型，如关系图视图、生成代码和其他项目的功能、用于转换模型的命令，以及在 Visual Studio 中与代码和其他对象进行交互的能力。 在开发模型时，你可以将其与其他模型和工具结合以形成一个以开发为中心的功能强大的工具集。

MSDK 允许你以域特定语言 (DSL) 的形式快速开发模型。 首先使用专用编辑器来将架构或抽象语法与图形表示法一起定义。 根据此定义，VMSDK 将生成：

- 使用运行于基于事务的存储内的强类型 API 的模型实现。

- 一个基于树的资源管理器。

- 一个图形编辑器，用户可在其中查看你定义的模型或其各个部分。

- 以可读的 XML 形式保存模型的序列化方法。

- 使用文本模板化生成程序代码和其他项目的设施。

你可以自定义和扩展所有这些功能。 你的扩展以某种方式集成，以使你仍能更新 DSL 定义并重新生成功能而不丢失扩展。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

[相关博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)