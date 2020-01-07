---
title: XML 架构资源管理器中的排序、筛选和分组
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4a914de0-9ffc-4526-9603-92e460e52513
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd288171cd8713e6b403f71a4eee6ba09d3f6ea9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592511"
---
# <a name="sorting-filtering-and-grouping-xml-schema-explorer"></a>排序、筛选和分组（XML 架构资源管理器）

本主题介绍通过**XML 架构资源管理器**工具栏上的 "**排序、筛选和分组选项**" 菜单可用的选项。

## <a name="filter-options"></a>筛选器选项

下列筛选器选项可用。 默认情况下，"**显示命名空间**" 和 "**显示架构文件**" 选项处于选中状态。

- **显示命名空间**。

- **显示架构文件**。

- **显示排序器（sequence/choice/all）** 。

## <a name="sorting-options"></a>排序选项

下列排序选项可用。 默认值为**按类型排序**。 "**排序依据**" 选项不适用于文件和命名空间。

- **按类型排序**。

- **按名称排序**。

- **文档顺序**。

### <a name="sort-by-type"></a>按类型排序

选中 "**按类型排序**" 选项后，全局节点将按以下顺序进行排序。 然后，节点将在每个组中按字母顺序进行排序。

1. `import` 节点。

2. `include` 节点。

3. `redefine` 节点。

4. `attribute` 节点。

5. `attributeGroup` 节点。

6. `complexType` 节点。

7. `simpleType` 节点。

8. `element` 节点。

9. `group` 节点。

### <a name="sort-by-name"></a>按名称排序

选择 "**按名称排序**" 选项后，全局节点将按以下顺序进行排序：

1. `import` 节点（按命名空间的字母顺序排序）。

2. `include` 节点（按 `schemaLocation` 特性的字母顺序）。

3. `redefine` 节点（按 `schemaLocation` 特性的字母顺序）。

4. 其他全局节点（按字母顺序）。

### <a name="document-order"></a>文档顺序

如果选择了 "**显示架构文件**" 选项，则可以使用 "**文档顺序**" 选项。 如果选择了 "**文档顺序**"，全局节点将按照它们在架构文件中的显示顺序显示。

## <a name="persisting-sortfilter-options"></a>持久化排序/筛选器选项

无论更改设置时打开的是哪个解决方案或文件，排序、筛选和分组选项均会保存到每个用户的注册表中。
