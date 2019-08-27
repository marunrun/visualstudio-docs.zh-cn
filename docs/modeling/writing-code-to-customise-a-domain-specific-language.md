---
title: 自定义特定于域的语言
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e62fa58d3f0678c8784cb8584a95d8475238ce0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62945435"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>编写代码以自定义域特定语言

本部分演示如何使用自定义代码来访问、 修改或在域特定语言中创建一个模型。

有几个可以在其中编写代码，它使用 DSL 的上下文：

- **自定义命令。** 可以创建命令，用户可以通过右键单击关系图中，调用以及其可以修改模型。 有关详细信息，请参阅[如何：将命令添加到快捷菜单](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)。

- **验证。** 可以编写代码，用于验证在模型处于正确状态。 有关详细信息，请参阅[特定于域的语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。

- **重写默认行为。** 您可以修改从 DslDefinition.dsl 生成的代码的许多方面。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。

- **文本转换。** 您可以编写文本模板包含的代码，以便访问模型，并生成一个文本文件，例如若要生成程序代码。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

- **其他 Visual Studio 扩展。** 您可以编写单独的 VSIX 扩展的读取和修改模型。 有关详细信息，请参阅[如何：在程序代码中从文件中打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)

在 DslDefinition.dsl 中定义的类的实例保存在名为的数据结构*内存中存储*(IMS) 或*存储区*。 你始终在 DSL 中定义的类构造函数作为自变量需要存储区。 例如，如果你的 DSL 定义一个名为示例类：

`Example element = new Example (theStore);`

使对象 （而不是只需为普通对象） 存储区中提供了以下几个好处。

- **事务**。 可以将一系列成事务相关的更改：

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     如果过程中发生异常所做的更改，以便不执行最终的 commit （），在存储区将重置为其以前的状态。 这可帮助你确保错误不会为不一致状态中保留该模型。 有关详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- **二进制关系**。 如果定义了两个类之间的关系，在两端的实例具有导航到另一端的属性。 两个端点始终保持同步。 例如，如果用名为父项和子项的角色定义 parenthood 关系时，您可以编写：

     `John.Children.Add(Mary)`

     这两个以下表达式现，则返回 true:

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     此外可以通过编写达到同样的效果：

     `Mary.Parents.Add(John)`

     有关详细信息，请参阅[导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- **规则和事件**。 可以定义指定更改时触发的规则。 规则使用，例如，要保留它们在呈现的模型元素保持最新关系图上的形状。 有关详细信息，请参阅[对的响应并传播更改](../modeling/responding-to-and-propagating-changes.md)。

- **序列化**。 在存储区提供一个标准的方式进行序列化到文件及其包含的对象。 您可以自定义序列化和反序列化规则。 有关详细信息，请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)。

## <a name="see-also"></a>请参阅

- [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)