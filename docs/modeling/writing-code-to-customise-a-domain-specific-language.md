---
title: 自定义域特定语言
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b67a50623eb1924c4a18b57524c409f7eba6ab20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546869"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>编写代码以自定义域特定语言

本部分说明如何使用自定义代码来访问、修改或创建域特定语言的模型。

可以通过多种上下文编写适用于 DSL 的代码：

- **自定义命令。** 您可以创建一个命令，用户可以通过右键单击该关系图，并可以修改模型。 有关详细信息，请参阅 [如何：向快捷菜单中添加命令](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)。

- **验证。** 您可以编写代码来验证模型是否处于正确的状态。 有关详细信息，请参阅 [以域特定语言进行验证](../modeling/validation-in-a-domain-specific-language.md)。

- **重写默认行为。** 您可以修改从 Dsldefinition.dsl 生成的代码的许多方面。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。

- **文本转换。** 您可以编写包含访问模型的代码的文本模板并生成文本文件，例如生成程序代码。 有关详细信息，请参阅 [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

- **其他 Visual Studio 扩展。** 可以编写用于读取和修改模型的单独的 VSIX 扩展。 有关详细信息，请参阅 [如何：在程序代码中从文件打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)

在 Dsldefinition.dsl 中定义的类的实例将保存在一个名为 *内存中存储* (IMS) 或 *存储*的数据结构中。 在 DSL 中定义的类始终将存储用作构造函数的参数。 例如，如果 DSL 定义了一个名为 Example 的类：

`Example element = new Example (theStore);`

将对象保存在存储区中 (，而不是像普通对象一样) 提供多个优点。

- **Transactions**。 可以将一系列相关更改分组到一个事务中：

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     如果在更改期间发生异常，因此不执行最终的提交 ( # A1，则存储将重置为其以前的状态。 这有助于确保错误不会使模型处于不一致状态。 有关详细信息，请参阅 [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- **二元关系**。 如果在两个类之间定义关系，则两端的实例都有一个导航到另一个端的属性。 这两个端点始终同步。 例如，如果使用名为 "父级" 和 "子级" 的角色定义 parenthood 关系，则可以编写：

     `John.Children.Add(Mary)`

     以下两个表达式现在为 true：

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     你还可以通过编写来实现同样的效果：

     `Mary.Parents.Add(John)`

     有关详细信息，请参阅 [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- **规则和事件**。 你可以定义在进行指定的更改时触发的规则。 例如，使用规则将关系图上的形状与它们提供的模型元素保持最新。 有关详细信息，请参阅 [响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

- **序列化**。 存储提供了一种标准方式来将其包含的对象序列化到文件中。 您可以自定义用于序列化和反序列化的规则。 有关详细信息，请参阅 [自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)。

## <a name="see-also"></a>另请参阅

- [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)