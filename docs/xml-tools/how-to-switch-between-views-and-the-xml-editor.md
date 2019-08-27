---
title: 如何：交换机之间视图和 XML 编辑器
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: cb69fbbd-d99c-439e-9498-5df9050f8df0
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 35839f8ae33068333259b30015e4cae0bb9c26d3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001825"
---
# <a name="how-to-switch-between-views-and-the-xml-editor"></a>如何：在视图和 XML 编辑器之间切换

本主题演示如何在 XML 架构设计器 （XSD 设计器） 视图和 XML 编辑器之间切换。 此示例使用[采购订单架构](../xml-tools/sample-xsd-file-simple-schema.md)。

## <a name="to-switch-between-the-views-and-the-xml-editor"></a>若要在视图和 XML 编辑器之间切换

1. 若要创建和编辑新的 XML 架构文件，请按照中的步骤[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)。

2. 若要从 XML 编辑器切换到 XML 架构设计器，右键单击 XML 编辑器中的任意位置并选择**视图设计器**。

3. 若要切换到使用水印的图形视图，请单击**使用关系图视图来查看节点之间的关系**起始视图上的链接。

4. 拖动`USAddress`节点从**XML 架构资源管理器**拖至关系图视图上。 右键单击`USAddress`在关系图视图中，选择节点**在内容模型视图中显示**的上下文菜单中。

     将显示包含 `USAddress` 节点详细信息的内容模型视图。

5. 若要从使用工具栏在内容模型视图切换到起始视图，请单击**起始视图**XSD 工具栏上的按钮。

6. 若要使用热键在视图之间切换，按**Ctrl**+**1**的启动视图中， **Ctrl**+**2**对于关系图视图中，并**Ctrl**+**3**内容模型视图。

7. 若要从内容模型视图转到 XML 编辑器，请右键单击节点并选择**查看代码**的上下文菜单中。