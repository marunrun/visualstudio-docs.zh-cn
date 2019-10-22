---
title: 域特定语言工具的概述
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 899fc041df3f7118de6be97309e8ce971235d178
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658321"
---
# <a name="overview-of-domain-specific-language-tools"></a>域特定语言工具的概述
在 Visual Studio 中托管的特定于域的语言工具（DSL 工具）使你可以设计域特定语言，然后生成用户创建基于语言的模型时必须具有的所有内容。

 DSL 工具包含以下工具：

- 项目向导 - 可使用各种解决方案模板帮助你开始开发域特定语言。

- 图形设计器 - 用于创建和编辑域特定语言定义。

- 验证引擎 - 可确保域特定语言定义的格式正确，并在出现问题时显示错误和警告。

- 代码生成器 - 获取域特定语言定义作为输入，并产生源代码作为输出。

## <a name="the-dsl-tools-solution"></a>DSL 工具解决方案
 域特定设计器向导提供以下解决方案模板：

- 任务流

- 类图

- 最小语言

- 组件模型

- 最小 WPF

- 最小 Windows.Forms

- DSL 库

  有关详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

  向导将创建一个具有以下项目的 Visual Studio 解决方案：

- DSL

   DSL 项目定义域特定语言及其编辑和处理工具。

- **DslPackage**

   DslPackage 项目确定语言工具如何与 Visual Studio 集成。

## <a name="the-dsl-tools-graphical-interface"></a>DSL 工具的图形界面
 DSL 工具的图形界面可用于将元素和关系添加到你的域特定语言。 添加元素后，可以通过将元素映射到形状、自定义颜色和添加修饰器来定义外观。 还可以向工具箱添加元素。

## <a name="validation-in-dsl-tools"></a>DSL 工具中的验证
 DSL 提供一个级别的验证，以确保域模型满足代码生成的基本要求。 通常情况下，在创建自己的域特定语言后，将添加自己的验证来表达业务逻辑规则。 有关自定义验证的详细信息，请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。

 我们建议你在设计域特定语言时经常验证它。 如果你的域特定语言出现验证错误，则无法生成源代码。 通过单击解决方案资源管理器的工具栏中的“转换所有模板”，执行根据模板生成源代码的过程。 只要是修改语言定义，都请确保转换所有模板。 有关详细信息，请参阅[如何：创建特定于域的语言解决方案](../modeling/how-to-create-a-domain-specific-language-solution.md)。

## <a name="customization-of-dsl-tools"></a>DSL 工具的自定义
 你可以提供其他代码来优化模型的行为和定义对语言的约束。 如果需要，可以通过修改文本模板进行重大更改。

## <a name="distributing-your-dsl-solution"></a>分发 DSL 解决方案
 DSL 工具会生成一个托管在 Visual Studio 中的包。 该程序包将显示一个工具箱、一个 DSL 资源管理器以及帮助用户使用你的域特定语言创建模型的其他 UI 元素。

 当你在 Visual Studio 中生成并运行 DSL 工具解决方案时，Visual Studio 的第二个实例将显示特定于域的语言对语言用户的外观。 验证一切运行正常之后，可以分发 DslPackage 项目的生成文件夹中的 `.vsix` 文件。 此文件可用于将 DSL 安装为其他计算机上的 Visual Studio 扩展。  有关详细信息，请参阅[部署域特定语言解决方案](msi-and-vsix-deployment-of-a-dsl.md)。

## <a name="see-also"></a>请参阅

- [实验实例](../extensibility/the-experimental-instance.md)
- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)