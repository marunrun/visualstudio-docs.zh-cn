---
title: 如何：在视图和 XML 编辑器之间切换
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: cb69fbbd-d99c-439e-9498-5df9050f8df0
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54e43b00c877f5453d1dc28bbc9d5546fcef056f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592616"
---
# <a name="how-to-switch-between-views-and-the-xml-editor"></a>如何：在视图和 XML 编辑器之间切换

本主题演示如何在 XML 架构设计器（XSD 设计器）视图和 XML 编辑器之间进行切换。 本示例使用[采购订单架构](../xml-tools/sample-xsd-file-simple-schema.md)。

## <a name="to-switch-between-the-views-and-the-xml-editor"></a>在视图和 XML 编辑器之间切换

1. 若要创建和编辑新的 XML 架构文件，请按照[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)中的步骤操作。

2. 若要从 XML 编辑器切换到 XML 架构设计器，请右键单击 XML 编辑器中的任意位置，并选择“视图设计器”  。

3. 若要切换到使用水印的图形视图，请单击起始视图上的“使用图形视图查看节点之间的关系”链接  。

4. 将 `USAddress` 节点从 XML 架构资源管理器拖到图形视图上  。 右键单击图形视图中的 `USAddress` 节点并在上下文菜单中选择“在内容模型视图中显示”  。

     将显示包含 `USAddress` 节点详细信息的内容模型视图。

5. 若要使用工具栏从内容模型视图切换到起始视图，请单击 XSD 工具栏上的“起始视图”按钮  。

6. 若要使用热键在视图之间切换，可按 Ctrl+1 切换到起始视图，按 Ctrl+2 切换到图形视图，按 Ctrl+3 切换到内容模型视图       。

7. 若要从内容模型视图转到 XML 编辑器，请右键单击节点并选择上下文菜单中的“查看代码”  。
