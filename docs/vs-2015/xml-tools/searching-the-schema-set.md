---
title: 搜索架构集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ec1395e0-d03c-4130-810d-f2db656937bd
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1d388db50ae935ef85b720177bd31c832a353d31
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145179"
---
# <a name="searching-the-schema-set"></a>搜索架构集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 XML 架构资源管理器，您可以通过下列方式在架构集中执行搜索：  
  
- 关键字搜索。  
  
- 特定于架构的搜索。  
  
## <a name="keyword-search"></a>关键字搜索  
 通过输入中的子字符串执行关键字搜索**搜索架构集**的 XML 架构资源管理器工具栏上的文本框。  
  
 ![XML 架构资源管理器关键字搜索](../xml-tools/media/schemaexplorersearch.gif "SchemaExplorerSearch")  
  
 XML 架构资源管理器在架构集中搜索以下内容：  
  
- 与指定关键字匹配的任何 `name` 或 `ref` 特性。 这样，您可以按名称来查找元素、特性、类型等。  
  
- 包括语句的 `schemaLocation` 特性。  
  
- 导入语句的 `namespace` 特性。  
  
## <a name="schema-specific-search"></a>特定于架构的搜索  
 XML 架构资源管理器中还包含一些内置搜索，可使用 XML 架构资源管理器的上下文菜单访问这些搜索。 有关可用的上下文菜单的详细信息，请参阅[上下文菜单](../xml-tools/context-menus-xml-schema-explorer.md)。 此外可以从起始视图; 执行特定于架构的搜索有关详细信息，请参阅中的"架构集详细信息"部分[起始视图](../xml-tools/start-view.md)主题。  
  
## <a name="displaying-and-navigating-search-results"></a>显示和导航搜索结果  
 完成搜索后，摘要结果窗格会添加到工具栏中，其中显示搜索的结果。 搜索结果还会突出显示在 XML 架构资源管理器中，并用垂直滚动条上的刻度标记。 可以通过使用导航搜索结果**转到下一个搜索结果**并**转到上一个搜索结果**摘要结果窗格; 通过使用键盘键的 XML 架构资源管理器工具栏上的按钮F3 和 Shift + F3;或单击滚动条中的刻度。  
  
 可以通过单击到工作区添加搜索结果**突出显示的节点添加到工作区**摘要结果窗格上的按钮。  
  
 ![XML 架构资源管理器搜索结果](../xml-tools/media/schemaexplorersearchresult.gif "SchemaExplorerSearchResult")  
  
## <a name="clearing-search-results"></a>清除搜索结果  
 若要清除搜索结果，请单击**x**摘要结果窗格中的 XML 架构资源管理器搜索工具栏按钮。  
  
## <a name="see-also"></a>请参阅  
 [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)
