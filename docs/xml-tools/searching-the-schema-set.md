---
title: XML 架构资源管理器-搜索架构集
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ec1395e0-d03c-4130-810d-f2db656937bd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 898b79e53773c09d60e32a3ef262346b0371d2af
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926804"
---
# <a name="search-the-schema-set"></a>搜索架构集

**XML 架构资源管理器**使您能够通过以下方式搜索架构集:

- 关键字搜索。

- 特定于架构的搜索。

## <a name="keyword-search"></a>关键字搜索

您可以通过在 " **XML 架构资源管理器**" 工具栏的 "**搜索 SchemaSet** " 文本框中输入一个子字符串来执行关键字搜索。

![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif)

**XML 架构资源管理器**会在架构集中搜索以下属性:

- 与指定关键字匹配的任何 `name` 或 `ref` 特性。 可以按名称查找元素、属性、类型等。

- 包括语句的 `schemaLocation` 特性。

- 导入语句的 `namespace` 特性。

## <a name="schema-specific-search"></a>架构特定的搜索

**Xml 架构资源管理器**还包括可使用**XML 架构资源管理器**的上下文 (右键单击) 菜单访问的内置搜索。 有关可用上下文菜单的详细信息, 请参阅[上下文菜单](../xml-tools/context-menus-xml-schema-explorer.md)。 你还可以从 "开始" 视图执行特定于架构的搜索;有关详细信息, 请参阅 "[开始视图](../xml-tools/start-view.md)" 主题中的 "架构集详细信息" 部分。

## <a name="display-and-navigate-search-results"></a>显示和导航搜索结果

完成搜索后，摘要结果窗格会添加到工具栏中，其中显示搜索的结果。 搜索结果还会突出显示在**XML 架构资源管理器**中, 并通过垂直滚动条上的刻度标记。 您可以使用 "**转到下一个搜索结果**" 导航搜索结果, 然后转到 " **XML 架构资源管理器**" 工具栏的摘要结果窗格上的 "**上一搜索结果**" 按钮;通过使用键盘键**f3**和**Shift**+**f3**, 或单击滚动条中的刻度线。

可以通过单击摘要结果窗格上的 "**将突出显示的节点添加到工作区**" 按钮, 将搜索结果添加到工作区。

![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif)

## <a name="clear-search-results"></a>清除搜索结果

若要清除搜索结果, 请单击 " **XML 架构资源管理器**搜索" 工具栏的 "摘要结果" 窗格中的**x**按钮。

## <a name="see-also"></a>请参阅

- [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)