---
title: 如何：添加或移除导入的命名空间 (Visual Basic)
ms.date: 06/21/2017
ms.topic: conceptual
helpviewer_keywords:
- adding imported namespaces
- removing imported namespaces
- namespaces [Visual Studio], imported
- imported namespaces [Visual Studio]
- references [Visual Studio], imported namespaces
ms.assetid: 44cebec3-0ea0-47c2-8406-4edeab6a997e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e636969164c4cf2526bb85add95e7cfe02ce6176
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75593325"
---
# <a name="how-to-add-or-remove-imported-namespaces-visual-basic"></a>如何：添加或移除导入的命名空间 (Visual Basic)

通过导入命名空间，可在代码中使用来自该命名空间的元素，而不必完全限定该元素。 例如，若要访问 `System.Messaging.MessageQueue` 类中的 `Create` 方法，可以导入 `System.Messaging` 命名空间，并引用代码中所需的元素作为 `MessageQueue.Create`。

导入的命名空间托管在“项目设计器”的“引用”页上   。 在此对话框中指定的导入会直接传递到编译器 (/imports) 中，并应用到项目的所有文件  。 使用 `Imports` 语句在单个源代码文件中使用命名空间。

### <a name="to-add-an-imported-namespace"></a>添加导入的命名空间

1. 在“解决方案资源管理器”中，双击项目的“我的项目”节点   。

2. 在“项目设计器”中，单击“引用”选项卡   。

3. 在“导入的命名空间”列表中，选中要添加的命名空间对应的复选框  。

    > [!NOTE]
    > 为了能够完成导入，命名空间必须位于引用组件中。 如果列表中未显示命名空间，需要添加对包含该命名空间的组件的引用。 有关详细信息，请参阅[管理项目中的引用](managing-references-in-a-project.md)。

### <a name="to-remove-an-imported-namespace"></a>移除导入的命名空间

1. 在“解决方案资源管理器”中，双击项目的“我的项目”节点   。

2. 在“项目设计器”中，单击“引用”选项卡   。

3. 在“导入的命名空间”列表中，清除要移除的命名空间对应的复选框  。

## <a name="user-imports"></a>用户导入
借助用户导入，可以导入命名空间内的特定类，而不能导入整个命名空间。 例如，应用程序可能具有 <xref:System.Diagnostics> 空间的导入，但在该命名空间内你唯一感兴趣的类是 `Debug` 类。 可以将 <xref:System.Diagnostics.Debug> 定义为用户导入，然后移除 <xref:System.Diagnostics> 的导入。

如果之后改变了主意，确定真正需要的是 `EventLog` 类，则可以输入 <xref:System.Diagnostics.EventLog> 作为用户导入并使用更新功能覆盖 <xref:System.Diagnostics.Debug>。

### <a name="to-add-a-user-import"></a>添加用户导入

1. 在“解决方案资源管理器”中，双击项目的“我的项目”节点   。

2. 在“项目设计器”中，单击“引用”选项卡   。

3. 在“导入的命名空间”列表下面的文本框中，输入要导入的命名空间的完整名称，包括根命名空间  。

4. 单击“添加用户导入”按钮，将命名空间添加到“导入的命名空间”列表   。

    > [!NOTE]
    > 如果该命名空间与列表中已存在的某个命名空间匹配，将禁用“添加用户导入”按钮；一个导入不能添加两次  。

### <a name="to-update-a-user-import"></a>更新用户导入

1. 在“解决方案资源管理器”中，双击项目的“我的项目”节点   。

2. 在“项目设计器”中，单击“引用”选项卡   。

3. 在“导入的命名空间”列表中，选中要更改的命名空间  。

4. 在“导入的命名空间”列表下面的文本框中，输入新命名空间的名称  。

5. 单击“更新用户导入”按钮，更新“导入的命名空间”列表中的命名空间   。

## <a name="see-also"></a>另请参阅

- [管理项目中的引用](../ide/managing-references-in-a-project.md)
